###java开发样例

* Send POST 以换取Access Token为例

```
    /*
     * Function  :   发送Post请求到服务器
     * Param     :   params参数，encode编码格式
     */
    public static void sendPost(Map<String, String> params, String encode) {
        byte[] data = getRequestData(params, encode).toString().getBytes();   //获得请求体
        try {            
    		URL url = new URL("https://huantengsmart.com/oauth2/token");
            HttpURLConnection httpURLConnection = (HttpURLConnection)url.openConnection();
            httpURLConnection.setConnectTimeout(3000);           //设置连接超时时间
            httpURLConnection.setDoInput(true);                  //打开输入流，从服务器获取数据
            httpURLConnection.setDoOutput(true);                 //打开输出流，向服务器提交数据
            httpURLConnection.setRequestMethod("POST");          //设置Post方式提交数据
            httpURLConnection.setUseCaches(false);               //使用Post方式不能使用缓存
            //设置请求体的类型是文本类型
            httpURLConnection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
            //设置请求体的长度
            httpURLConnection.setRequestProperty("Content-Length", String.valueOf(data.length));
            //获得输出流，向服务器写入数据
            OutputStream outputStream = httpURLConnection.getOutputStream();
            outputStream.write(data);

            int response = httpURLConnection.getResponseCode();            //获得服务器的响应码
            if(response == HttpURLConnection.HTTP_OK) {
            	//处理服务器的响应结果
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    /*
     * Function  :   封装请求体信息
     * Param     :   params请求体内容，encode编码格式
     */
    public static StringBuffer getRequestData(Map<String, String> params, String encode) {
        StringBuffer stringBuffer = new StringBuffer();        
        try {
            for(Map.Entry<String, String> entry : params.entrySet()) {
                stringBuffer.append(entry.getKey())
                            .append("=")
                            .append(URLEncoder.encode(entry.getValue(), encode))
                            .append("&");
            }
            stringBuffer.deleteCharAt(stringBuffer.length() - 1);    
        } catch (Exception e) {
            e.printStackTrace();
        }
        return stringBuffer;
    }
```

* Send GET 以获取授权为例

```
    /*
     * Function  :   发送Get请求到服务器
     * Param     :   params参数，encode编码格式
     */
    public static void sendPost(Map<String, String> params, String encode) {
        try {            
            URL url = new URL("https://huantengsmart.com/oauth2/authorize" + getRequestData(params, encode).toString());
            HttpURLConnection httpURLConnection = (HttpURLConnection)url.openConnection();
            httpURLConnection.setConnectTimeout(3000);           //设置连接超时时间
            //设置请求体的类型是文本类型
            httpURLConnection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
            int response = httpURLConnection.getResponseCode();            //获得服务器的响应码
            if(response == HttpURLConnection.HTTP_OK) {
                //处理服务器的响应结果
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
    /*
     * Function  :   封装参数
     * Param     :   params参数，encode编码格式
     */
    public static StringBuffer getRequestData(Map<String, String> params, String encode) {
        StringBuffer stringBuffer = new StringBuffer();        
        try {
            for(Map.Entry<String, String> entry : params.entrySet()) {
                stringBuffer.append(entry.getKey())
                            .append("=")
                            .append(URLEncoder.encode(entry.getValue(), encode))
                            .append("&");
            }
            stringBuffer.deleteCharAt(stringBuffer.length() - 1);    
        } catch (Exception e) {
            e.printStackTrace();
        }
        return stringBuffer;
    }
```
