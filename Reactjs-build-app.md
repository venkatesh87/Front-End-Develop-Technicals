### I. Setting
---
- Trong quá trình cài đặt dù đã chạy hết các câu lệnh yêu cầu nhưng source vẫn ko chạy được. Dưới đây là các câu lênh cần chạy thêm:

```javascript
npm install --save-dev webpack
npm install --save-dev cross-env
npm install "cross-env"
npm install -g win-node-env
```

- Trong file ```package.json``` nên thêm dòng này: 
```javascript
"scripts": {
  "build": "cross-env NODE_ENV=production webpack --config build/webpack.config.js"
}
```

### II. App
---
**1.**

```javascript

```


