# gitbook Debug

## Gitbook Debug Template render error

报错模板:

    error: error while generating page "VueRecords/VueBindVueRouterToMenu.md":

    Template render error: (D:\projects\workspace\liyf_gitbook\VueRecords\VueBindVueRouterToMenu.md) [Line 35, Column 20]
      expected variable end

解决:

查看 [GitbookIO Issue: Windows only "Template render error expected variable end](https://github.com/GitbookIO/gitbook/issues/1827)

简单来说, 当文档中出现双花括号时，会出现识别错误，此时需要声明双括号为原始代码(使用 `{% raw %}{% endraw %}` 包裹起来)，而非模板。

    For example:

    {% raw %}

    var Dialog = require('ysp-interior-components').Dialog;
    module.exports = React.createClass({

      getInitialState: function() {
        return { open: false };
      },

      handleClick: function() {
          this.setState({
            open: !this.state.open
        });
      },

      render: function() {
          return (
          <div>
            <AMUI.Button onClick={this.handleClick}>点我显示弹窗</AMUI.Button>
            {this.state.open &&
              <Dialog config={{status: "real"}}>
                <h4 className="modal-title">Modal 标题</h4>
                <span onClick={this.handleClick} className="icon icon-close modal-icon"></span>
                <div className="modal-body">Hello, Modal 内容</div>
              </Dialog>}
          </div>
        );
      }
    });
    {% endraw %}
