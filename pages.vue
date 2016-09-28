<template>
    <div class="ui pagination menu">
        <a class="item icon" title="首页" v-if="now > 1" @click="go(1)">
            <i class="icon left arrow"></i>
        </a>

        <a class="item" :class="{active: num === now}"
           v-for="num of nums"
           @click="go(num)">{{num}}</a>

        <a class="item icon" title="末页" v-if="now < total_page" @click="go(total_page)">
            <i class="icon right arrow"></i>
        </a>

        <span class="item">共 {{total}} 条</span>
    </div>
</template>

<script>
    export default {
        props: {
            ext: {
                type: [Number],
                default: 3
            },
            size: {
                type: [Number],
                default: 20
            },
            total: {
                type: [Number],
                required: true
            },
            page: {
                type: [Number, String],
                default: 1
            }
        },
        computed: {
            now() {
                return parseInt(this.page, 10) || 1;
            },
            total_page() {
                return Math.ceil(this.total / this.size);
            },
            nums() {
                let nums = [this.now];
                let after = this.now <= this.ext ? this.ext - this.now + 1 : 0;
                let before = this.total_page - this.now < this.ext ? this.ext - (this.total_page - this.now) : 0;
                if (!this.total_page) {
                    before = 0;
                }
                for (let i = this.now - 1; this.now - i <= this.ext + before && i > 0; i--) {
                    nums.unshift(i);
                }
                for (let i = this.now + 1; i - this.now <= this.ext + after && i <= this.total_page; i++) {
                    nums.push(i);
                }
                return nums;
            }
        },
        methods: {
            go(num) {
                if (num !== this.now) {
                    this.$emit('get', num);
                }
            }
        },
        ready() {
            this.$emit('get', this.now);
        }
    }
</script>
