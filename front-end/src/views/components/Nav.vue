<template>
    <div>
        <ul :class="['nav', { 'nav-fixed': !isTop, 'nav-invisible': !isVisible }]">
            <li>
                <router-link class="item" :to="{name: 'Index'}">主页</router-link>
            </li>
            <li>
                <router-link class="item" :to="{name: 'about'}">关于</router-link>
            </li>
            <li>
                <router-link class="item" :to="{name: 'tags'}">标签</router-link>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                nav: 'nav',
                isTop: true,
                isVisible: true
            }
        },
        created() {
            this.scroll()
        },
        methods: {
            scroll() {
                let beforeScrollTop = document.body.scrollTop
                window.onscroll = () => {
                    const afterScrollTop = document.body.scrollTop
                    const delta = afterScrollTop - beforeScrollTop
                    this.isTop = afterScrollTop === 0
                    if (delta === 0) return false
                    beforeScrollTop = afterScrollTop
                    this.isVisible = delta <= 0
                    if (afterScrollTop < 48) {
                        this.isVisible = true
                    }
                }
            }
        }
    }
</script>

<style lang="scss">
    .nav {
        position: fixed;
        width: 100%;
        display: flex;
        -webkit-flex-flow: row wrap;
        justify-content: flex-end;
        background-color: rgba(0, 0, 0, 0);
        transition: all .4s;
        list-style: none;
        z-index: 100;
        .item {
            font-size: 1.2rem;
            display: block;
            margin: 0;
            padding: 1rem 1.2rem;
            opacity: 1;
            transition: opacity 0.4s;
            cursor: pointer;
            color: #fff;
        }
    }
    
    .nav-fixed {
        background-color: rgba(255, 255, 255, 0.95);
        border-bottom: 1px solid #bababa;
        z-index: 1;
        .item {
            color: rgba(0, 0, 0, .8);
        }
    }
    
    .nav-invisible {
        transform: translate(0, -4rem)
    }
    
    .nav a:hover {
        opacity: 0.7;
    }
</style>