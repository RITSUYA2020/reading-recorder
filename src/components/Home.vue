<template>
    <div class="list">
        <p> {{ bookCount }}件の読書情報が記録されています。</p>
        <!-- 書籍情報を一覧表示 (キーはid) -->
        <BookInfo v-for="(b, i) of books" :linkable="true" :book="b" :index="i + 1" :key="b.id"></BookInfo>
        <!-- ページャーを生成 -->
        <div>
            <el-pagination background layout="prev, pager, next"
            :total="bookCount" :page-size="3" @current-change="onchange">
            </el-pagination>
        </div>
    </div>
</template>

<script>
import { mapGetters } from 'vuex';
import BookInfo from '@/components/BookInfo.vue'

export default {
    name: 'home',
    // booksは登録済みのレビュー情報 (配列)
    data() {
        return {
            books: []
        }
    },
    components: {
        BookInfo
    },
    // ゲッターを算出プロパティに紐付け
    computed: mapGetters([ 'bookCount', 'getRangeByPage' ]),
    methods: {
        // ページが変更された場合に、現在ぺージ用のレビュー情報を再セット
        onchange(page) {
            this.books = this.getRangeByPage(page)
        }
    },
    // 初期化（マウント）時に1ページ目のレビュー情報を取得
    mounted() {
        this.books = this.getRangeByPage(1)
    }
}
</script>
