欲买桂花同载酒 终不似 少年游
// 增加api代理地址后的配置
// ...... 其他配置
"translationServices": {
    "deepl": {
      "authKey": "12345678-1234-5678-40f1-0f4bfc96f3c0", // 这里的authKey可以乱写1234，但必须要有!
      "freeApiUrl": "https://api-free.deeplx.net", // 这里是增加的部分
      "proApiUrl": "https://api-free.deeplx.net" // 这里是增加的部分
    },
    "deeplx": {
      "limit": "30",
      "url": "http://localhost:1188/translate"
    },
    // ...... 其他翻译服务
}