# mongoose

## 简介

## 消除弃用警告

mongoose 有些接口被弃用或不建议使用，Node.js驱动时会发出`DeprecationWarning`警告，

- `mongoose.set('useNewUrlParser', true);`
- `mongoose.set('useFindAndModify', false);`
- `mongoose.set('useCreateIndex', true);`
- 更换`update()`用`updateOne()`，`updateMany()`或`replaceOne()`
- 替换`remove()`为`deleteOne()`或`deleteMany()`。
- 替换`count()`为`countDocuments()`，除非您想要计算整个集合中有多少文档（没有过滤器）。在后一种情况下，使用`estimatedDocumentCount()`。

## api

- Model.findById()
  - 通过`_id`字段查找单个文档。`findById(id)`差不多相当于`findOne({ _id: id })`。如果要按文档查询`_id`，请使用`findById()`而不是`findOne()`。

## 替换_id

```js
toJSON: {
    // virtuals: true,
    transform: (doc, ret, options) => {
    // transfrom _id to id
    ret.id = ret._id;
    delete ret._id;
    return ret;
}}
```

## 连表查询

[Mongoose Populate 基本使用](https://blog.csdn.net/Elliott_Yoho/article/details/53537147)

## 数组添加元素

$addToSet：向数组中添加元素，若数组本身含有该元素，则不添加，否则，添加，这样就避免了数组中的元素重复现象；
$push：向数组尾部添加元素，但它不管数组中有没有该元素，都会添加。
