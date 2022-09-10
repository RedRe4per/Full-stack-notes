我刚才试了下。就那个关联的路径 url 中两个 id 的问题。

<font color='green'>结果是，其实并不需要给 _id 一个 alias 就能实现。反而，如果给 _id alians 的话会遇到一个问题，就是 type 值给什么？不填 type 值会报错。如果 type 值给 String 的话，就要自创 id 而不能用 mongoose 默认的 ObjectId。如果 type 值给 mongoose.Types.ObjectId, 用 postman 发请求时我记得也会报错的，还是要你自己指定 id 而不是 mongoose 生成。</font>

<font color='green'>然后我也试了给 id 一个 alias，还是不行，会报错，需要你自己生成 id。</font>



最后的解决方案是，直接不用管这个 _id 的名字。。。schema 中的 _id 名和你关联路径中的 :id 名可以不匹配。比如（router文件中）我是这么写的：

```javascript
subCategoryRouter.post('/:subCategoryId/rootCategory/:rootCategoryId', addRootCategoryToSubCategory)
```

url 路径是 `// POST  /v1/subCategory/:subCategoryId/rootCategory/:rootCategoryId`

而我的 controller 文件是这么写：

```javascript
async function addRootCategoryToSubCategory(req, res) {
    const { subCategoryId, rootCategoryId } = req.params;
    const subCategory = await SubCategory.findById(subCategoryId).exec();
    const rootCategory = await RootCategory.findById(rootCategoryId).exec();

    if (!subCategory || !rootCategory) {
        return res.status(404).json({
            error: 'Category or Subcategory not found',
        });
    }
    
    return res.json({
        'id 1':subCategoryId,     //能正常得到url中的subCategory的ID
        'id 2':rootCategoryId     //也能正常得到url中的rootCategoryId的ID
    });
```

相当于 :subCategoryId 和 :rootCategoryId 这两个字段只存在于 router 文件和 controller 文件中，完全不存在于 schema 文件中。schema 文件中没有任何关于 id 的操作和字段，只是使用 mongoose 默认的。

<font color='red'>所以结论就是，schema中不用取 alias，只需要在 router 和 controller 文件中分开两个 id 并且另行命名即可。</font>