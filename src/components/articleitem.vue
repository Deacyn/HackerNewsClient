<template>
    <article id="articleitemContent" class="hacker-article-item txt" v-link="" >
        <header>
            <div class="info-wrapper">
                <h2 class="article-list-title">
                    <a v-link="{path:'/contents?id='+item.id}" v-show="item.title">{{item.title}}</a>
                    <a v-link="{path:'/contents?id='+item.id}" v-show="!item.title">{{item.type}}</a>
                </h2>
                <div class="article-meta">
                    <span class="article-time" datetime="">{{item.score}} {{ item.score > 1 ? 'points' : 'point' }}</span>
                    <span class="article-tags">
                        <a class="tag" v-link="{path:'/contents?id='+item.id}">{{item.time | momentFromNow}}</a>
                        <a class="tag" v-link="{path:'/users?id='+item.by}">{{item.by}}</a>
                    </span>
                </div>
            </div>
        </header>
        <section class="article-excerpt">{{item.text | excerpt '50'}}
        </section>
        <footer>
            <div class="article-readmore">
                <a v-link="{path:'/contents?id='+item.id}" title="READ MORE">READ MORE »</a>
            </div>
        </footer>
    </article>
</template>
<script>
    import moment from "moment";
    export default {
        name: "articleitem",
        el: function(){
            return "#articleitemContent";
        },
        props: ["item"],
        filters: {
            moment: function (value, formatString) {
                formatString = formatString || 'YYYY-MM-DD HH:mm:ss';
                return moment(value).format(formatString);
            },
            momentFromNow: function (value, formatString) {
                formatString = formatString || '"YYYY';
                return moment(value, formatString).fromNow();
            },
            excerpt: function(value = "", formatString){
                return value.substr(0,Number(formatString));
            }
        }
    }
</script>

