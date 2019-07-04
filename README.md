get方法
function createObjectURL(object) { return (window.URL) ? window.URL.createObjectURL(object) : window.webkitURL.createObjectURL(object); }
            var xhr = new XMLHttpRequest();
            var formData = new FormData();
            xhr.open('get','url');  //url填写后台的接口地址，如果是post，在formData append参数（参考原文地址）
            xhr.setRequestHeader("access-token", sessionStorage.getItem('access-token'));
            xhr.responseType = 'blob';
            xhr.onload = function (e) {
                if (this.status == 200) {
                    var blob = this.response;
                    var filename = "设备导出.xls";
                    console.log(this.response)
                     if (window.navigator.msSaveOrOpenBlob) {
                        navigator.msSaveBlob(blob, filename);
                    } else {
                      var a = document.createElement('a');
                     var url = createObjectURL(blob);
                     a.href = url;
                     a.download = filename;
                     document.body.appendChild(a);
                     a.click();
                     window.URL.revokeObjectURL(url);
                    }
                    
                }
            };
            xhr.send(formData);
  
