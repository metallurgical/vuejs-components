<template>
    <nav aria-label="">
        <ul class="pagination">
            <li class="page-item" :class="{ 'disabled': paginate.current_page <= 1 }" v-if="isPrevPage">
                <a class="page-link" href="javascript: void(0);" tabindex="-1" @click="fetch(paginate.prev_page_url)">{{
                    prevText}}</a>
            </li>
            <li class="page-item"><a class="page-link" href="javascript: void(0);" v-if="isPrevPage" @click="fetch(paginate.path + '?page=' + prevPage)">{{ prevPage }}</a></li>
            <li class="page-item active">
                <a class="page-link" href="#">{{ paginate.current_page }} <span class="sr-only">(current)</span></a>
            </li>
            <li class="page-item"><a class="page-link" href="javascript: void(0);" v-if="isNextPage" @click="fetch(paginate.path + '?page=' + nextPage)">{{ nextPage }}</a></li>
            <li class="page-item" v-if="isNextPage">
                <a class="page-link" href="javascript: void(0);" @click="fetch(paginate.next_page_url)">{{ nextText
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

Available Props:
- prevText(string)
- nextText(string)
- paginate(object), laravel pagination instance

Event Listener:
- remote-call, parent component must pass in function's name for component able to call ajax request.

E.g: 

From child component will emit this event
this.$emit('remote-call', url)

From parent must passed in
<pagination :paginate="paginate" v-on:remote-call="getData"></pagination>

methods: {
  getData(url) {
      // call ajax request using axios or whatsoever
  }
}
