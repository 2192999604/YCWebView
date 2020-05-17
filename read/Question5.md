#### 问题汇总目录介绍
- 4.6.6 WebView如何隐藏H5的部分内容













### 4.6.6 WebView如何隐藏H5的部分内容
- 产品需求
    - 要在App中打开xx的链接，并且要隐藏掉H5页面的某些内容，这个就需要在Java代码中操作WebView，让H5页面加载完成后能够隐藏掉某些内容。
- 需要几个前提条件
    - 页面加载完成
    - 在Java代码中执行Js代码
    - 利用Js代码找到页面中的底部栏并将其隐藏
- 如何在h5中找隐藏元素
    - 在H5页面中找到某个元素还是有很多方法的，比如getElementById()、getElementsByClassName()、getElementsByTagName()等，具体根据页面来选择
    - 找到要隐藏的h5视图div，然后可以看到有id，或者class。这里用class举例子，比如div的class叫做'copyright'
    - document.getElementsByClassName('copyright')[0].style.display='none'
- 代码操作如下所示
    ```
    /**
     * 可以等页面加载完成后，执行Js代码，找到底部栏并将其隐藏
     * 如何找h5页面元素：
     *      在H5页面中找到某个元素还是有很多方法的，比如getElementById()、getElementsByClassName()、getElementsByTagName()等，具体根据页面来选择
     * 隐藏底部有赞的东西
     *      这个主要找到copyright标签，然后反射拿到该方法，调用隐藏逻辑
     * 步骤操作如下：
     * 1.首先通过getElementByClassName方法找到'class'为'copyright'的所有元素，返回的是一个数组，
     * 2.在这个页面中，只有底部栏的'class'为'copyright'，所以取数组中的第一个元素对应的就是底部栏元素
     * 3.然后将底部栏的display属性设置为'none'，表示底部栏不显示，这样就可以将底部栏隐藏
     *
     * 可能存在问题：
     * onPageFinished没有执行，导致这段代码没有走
     */
    private void hideBottom() {
        try {
            if (mWebView!=null) {
                //定义javaScript方法
                String javascript = "javascript:function hideBottom() { "
                        + "document.getElementsByClassName('copyright')[0].style.display='none'"
                        + "}";
                //加载方法
                mWebView.loadUrl(javascript);
                //执行方法
                mWebView.loadUrl("javascript:hideBottom();");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    ```




