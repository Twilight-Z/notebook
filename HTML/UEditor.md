# 百度UEditor去除自动p标签

首先：打开ueditor.all.js(或ueditor.all.min.js)。

1、搜索修改成false：allowDivTransToP: false

2、再搜索并修改以下：

//编辑器不能为空内容

if (domUtils.isEmptyNode(me.body)) {

me.body.innerHTML = '<div>' + (browser.ie ? '' : '<br/>') + '</div>';

}

3、搜索“/给文本或者inline节点套p标签”，并且替换以下内容

//给文本或者inline节点套p标签
```
if (me.options.enterTag == 'p') {
  var child = this.body.firstChild, tmpNode;
  if (!child || child.nodeType == 1 &&
    (dtd.$cdata[child.tagName] || isCdataDiv(child) ||
      domUtils.isCustomeNode(child)
      )
    && child === this.body.lastChild) {
    this.body.innerHTML = '<div>' + (browser.ie ? ' ' : '<br/>') + '</div>' + this.body.innerHTML;
  } else {
    var p = me.document.createElement('div');
    while (child) {
      while (child && (child.nodeType == 3 || child.nodeType == 1 && dtd.p[child.tagName] && !dtd.$cdata[child.tagName])) {
        tmpNode = child.nextSibling;
        p.appendChild(child);
        child = tmpNode;
      }
      if (p.firstChild) {
        if (!child) {
          me.body.appendChild(p);
          break;
        } else {
          child.parentNode.insertBefore(p, child);
          p = me.document.createElement('div');
        }
      }
      child = child.nextSibling;
    }
  }
}
```

4、搜索 “进入编辑器的li要套p标签”，这块也要注释掉

5、注视掉这段

node.className = utils.trim(node.className.replace(/list-paddingleft-\w+/,'')) + ' list-paddingleft-' + type;

6、最后注视掉：

li.style.cssText && (li.style.cssText = '');

完美解决，以上是整个流程。
