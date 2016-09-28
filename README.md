# vue-pages
Vue分页组件


![](https://raw.githubusercontent.com/Yusoo/vue-pages/master/pic.png)


# 使用

```html
<pages :page="param.page" :size="param.size" :total="total" @get="getList"></pages>
```



```js
 import pages from 'component/pages.vue';

    export default {
        data() {
            return {
                param: {
                    search: '',
                    size: 10,
                    page: 1
                },
                total: 0,
                rows: []
            }
        },
        methods: {
            getList(num) {
                this.param.page = num;
            }
        },
        components: {
            pages
        }
    }
```
