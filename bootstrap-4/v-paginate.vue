<template>
    <nav aria-label="">
        <ul class="pagination">
            <li class="page-item" :class="{ 'disabled': paginate.current_page <= 1 }" v-if="isPrevPage">
                <a class="page-link" tabindex="-1" @click.prevent="fetch(paginate.prev_page_url)">{{
                    prevText}}</a>
            </li>
            <li class="page-item"><a class="page-link" v-if="isPrevPage" @click.prevent="fetch(paginate.path + '?page=' + prevPage)">{{ prevPage }}</a></li>
            <li class="page-item active">
                <a class="page-link" href="javascript:void(0);">{{ paginate.current_page }} <span class="sr-only">(current)</span></a>
            </li>
            <li class="page-item"><a class="page-link" v-if="isNextPage" @click.prevent="fetch(paginate.path + '?page=' + nextPage)">{{ nextPage }}</a></li>
            <li class="page-item" v-if="isNextPage">
                <a class="page-link" @click.prevent="fetch(paginate.next_page_url)">{{ nextText
                    }}</a>
            </li>
        </ul>
    </nav>
</template>

<script>
    export default {
        props: {
            prevText: {
                type: String,
                default: 'Previous'
            },
            nextText: {
                type: String,
                default: 'Next'
            },
            paginate: {
                type: Object,
                default: {}
            }
        },
        data: function () {
            return {
                isNextPage: false,
                nextPage: 0,
                isPrevPage: false,
                prevPage: 0,
            }
        },
        methods: {
            fetch: function (url) {
                this.$emit('remote-call', url)
            }
        },
        updated() {
            if (this.paginate.next_page_url) {
                this.isNextPage = true;
                this.nextPage = this.paginate.current_page + 1;
            } else {
                this.isNextPage = false;
            }

            if (this.paginate.prev_page_url) {
                this.isPrevPage = true;
                this.prevPage = this.paginate.current_page - 1;
            } else {
                this.isPrevPage = false;
            }
        }
    }
</script>
