# Print-Browser
---
适用于React框架

由于React是虚拟Dom，之前查资料的方式再返回DOM的事件都不生效了

经过验证可以通过iframe新建一个浏览器生成的print之后就不会影响打

同时还可以实现局部打印效果

JS部分
```JS

  handlePrint(){
      let printContent =  document.getElementById('table').getElementsByTagName('table')[0].innerHTML;//实现获取局部内容打印
      printContent=(`<table  border="1" cellspacing="0">${printContent}`); 
      const frame = document.getElementById('printWrap');
      frame.contentDocument.write(printContent);//防止打印完Dom事件不生效
      frame.contentDocument.close();
      frame.contentWindow.print();
  };

````

HTML部分

以引用ANTD的table举例
```React
import {Table } from 'antd';
   return (
      <Fragment>
        <Spin spinning={!!loading} />        
              <Table 
                bordered
                id="table"
                columns={columns}
                dataSource={dataSource}
                pagination={false}
              />
            </div>
       
        <iframe title="print" id="printWrap" src="" width="0" height="0" frameBorder="0" />
      </Fragment>
    )
  }
}
```
