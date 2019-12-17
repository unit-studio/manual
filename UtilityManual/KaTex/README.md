# KaTex

## 相关文档

查看:

* [wikibooks LaTeX/Mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics)

* [在 gitbook 中使用数学公式](https://598753468.gitbooks.io/tex/content/)

## 举例

### 1. 双$ 符, 行内展示

输入

```
$$ a^{b} $$
```

输出为:

$$ a^{b} $$

输入

```
$$ \forall x \in X, \quad \exists y \leqslant \epsilon $$
```

输出为:

$$ \forall x \in X, \quad \exists y \leqslant \epsilon $$


### 2. math 符, 块式显示

输入

```
{% math %}
  a^{b}
{% endmath %}
```

输出为:

{% math %}
  a^{b}
{% endmath %}

输入

```
{% math %}
  \forall x \in X, \quad \exists y \leqslant \epsilon
{% endmath %}
```

输出为:

{% math %}
  \forall x \in X, \quad \exists y \leqslant \epsilon
{% endmath %}
