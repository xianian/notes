* http请求 
    一个http请求包括三个部分，为别为请求行，请求报头，消息主体
    HTTP协议规定post提交的数据必须放在消息主体中，但是协议并没有规定必须使用什么编码方式。服务端通过是根据请求头中的Content-Type字段来获知请求中的消息主体是用何种方式进行编码，再对消息主体进行解析。具体的编码方式包括：
    - application/x-www-form-urlencoded 最常见post提交数据的方式，以form表单形式提交数据。
    - application/json 以json串提交数据。
    - multipart/form-data 一般使用来上传文件。
