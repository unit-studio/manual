# Vue 打印部分页面 jsPdf 篇

## jsPdf

```js
// 导出页面为PDF格式
import html2Canvas from "html2canvas";
import JsPDF from "jspdf";
export default {
  install(Vue, options) {
    Vue.prototype.getPdf = function(
      documentId = "#pdfDom",
      options = {
        htmlTitle: "exportPdf",
        zoom: 1
      },
      callback = () => {}
    ) {
      let _this = this,
        { htmlTitle, zoom } = options;

      if (!zoom) {
        zoom = 1;
      }

      var title = htmlTitle || this.htmlTitle || "exportPdf";
      let gotHtml = document.querySelector(documentId);

      this.$confirm(
        "<p>1. 页面缩放为 100% </p><p>2. 开发者工具已关闭 </p>",
        "打印前请检查",
        {
          confirmButtonText: "确定",
          cancelButtonText: "取消",
          type: "warning",
          dangerouslyUseHTMLString: true
        }
      )
        .then(() => {
          gotHtml.style.zoom = zoom;
          let initMarginTop = gotHtml.style.marginTop;
          gotHtml.style.marginTop = "100px";

          // 增大canvas的宽高,将所形成的图片分辨率提高,以此来降低图片的失真度
          var shareContent = gotHtml;
          var width = shareContent.offsetWidth;
          var height = shareContent.offsetHeight;
          var canvas = document.createElement("canvas");
          var canvasScale = 3;

          canvas.width = width * canvasScale;
          canvas.height = height * canvasScale;
          canvas.getContext("2d").scale(canvasScale, canvasScale);

          // 设置canvas图
          var opts = {
            scale: canvasScale,
            canvas: canvas,
            logging: true,
            width: width,
            height: height
          };

          html2Canvas(gotHtml, opts).then(function(canvas) {
            let contentWidth = canvas.width;
            let contentHeight = canvas.height;
            let pageHeight = (contentWidth / 592.28) * 841.89;
            let leftHeight = contentHeight;
            let position = 0;
            // let imgWidth = 595.28   // 原来的设置
            let imgWidth = 495.28;
            // let imgHeight = 592.28 / contentWidth * contentHeight   // 原来的设置
            let imgHeight = (492.28 / contentWidth) * contentHeight;
            let pageData = canvas.toDataURL("image/jpeg", 1.0);
            let PDF = new JsPDF("", "pt", "a4");
            if (leftHeight < pageHeight) {
              // PDF.addImage(pageData, 'JPEG', 0, 0, imgWidth, imgHeight)  // 原来的设置
              PDF.addImage(pageData, "JPEG", 50, 10, imgWidth, imgHeight);
            } else {
              while (leftHeight > 0) {
                // PDF.addImage(pageData, 'JPEG', 0, position, imgWidth, imgHeight)  // 原来的设置
                PDF.addImage(
                  pageData,
                  "JPEG",
                  50,
                  position,
                  imgWidth,
                  imgHeight
                );
                leftHeight -= pageHeight;
                position -= 841.89;
                if (leftHeight > 0) {
                  PDF.addPage();
                }
              }
            }

            // 设置自动打印,指的是当打开此文件或者在页面中加载此文件时,进行自动的打印预览,并进行打印
            // PDF.autoPrint({
            // variant: 'javascript'
            // })
            // console.log(PDF);

            let pdfBlob = PDF.output("blob", {
              filename: title
            });

            let windowSrc = URL.createObjectURL(
              new Blob([pdfBlob], {
                type: "application/pdf"
              })
            );

            /**** 打印方式1(务必配合上述 PDF.autoPrint() 函数,否则打印出不来,只是单纯的向页面添加了一个东西): 在当前页面直接打印; 坏处是在一些没有打印预览的浏览器上,看不出要打印的是什么! ****/
            // 已经设置过主动打印,当将iframe加载到窗口中时,就会自动进行打印,这样避免了打开新的窗口
            // let iframe = document.createElement('iframe');
            // iframe.src = windowSrc;
            // document.getElementById('temporaryDom').appendChild(iframe);

            /**** 打印方式2(可禁用 PDF.autoPrint() ): 在新的窗口进行打印,这样弥补了 1 的不足,但是要开新窗口 ****/
            // 看一看直接进行新窗口打印好不好使
            // 卧槽,这个是好使的!
            window.open(windowSrc, title);

            /**** 打印方式3(可禁用 PDF.autoPrint() ): 导出文件,然后打开文件,进行打印 ****/
            // 将文件以 pdf 的格式进行保存
            // PDF.save(title + '.pdf')

            gotHtml.style.marginTop = initMarginTop;
            gotHtml.style.zoom = 1;

            callback();
          });
        })
        .catch(() => {
          this.errorMessage("取消打印");
        });
    };
  }
};
```
