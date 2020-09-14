<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">
              Home
              <span class="sr-only">(current)</span>
            </a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Link</a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdown"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >Dropdown</a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdown">
              <a class="dropdown-item" href="#">Action</a>
              <a class="dropdown-item" href="#">Another action</a>
              <div class="dropdown-divider"></div>
              <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" href="#">Disabled</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input
            class="form-control mr-sm-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
          />
          <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
        </form>
      </div>
    </nav>

    <div class="container">
      <h1>こんにちは</h1>
      <button type="button" @click="func1" class="btn btn-primary">Primary</button>
      <button type="button" @click="test_method" class="btn btn-primary">実行2</button>

      <table class="table">
        <thead class="thead-light">
          <tr>
            <th scope="col">タイトル</th>
            <th scope="col">著者</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="book in books" v-bind:key="book.id">
            <td>{{ book.title }}</td>
            <td>{{ book.author }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      books: [
        { id: 1, title: "坊っちゃん", author: "夏目漱石" },
        { id: 2, title: "人間失格", author: "太宰治" },
        { id: 3, title: "ノルウェイの森", author: "村上春樹" },
      ],
    };
  },
  methods: {
    func1() {
      this.books = [
        { id: 1, title: "坊っちゃん3", author: "夏目漱石" },
        { id: 2, title: "人間失格", author: "太宰治" },
        { id: 3, title: "ノルウェイの森", author: "村上春樹" },
      ];
    },
    func2() {
      this.books = [
        { id: 1, title: "坊っちゃん2", author: "夏目漱石" },
        { id: 2, title: "人間失格", author: "太宰治" },
        { id: 3, title: "ノルウェイの森", author: "村上春樹" },
      ];
    },
    async test_method() {
      const res = await this.$axios.$get("https://qiita.com/api/v2/items");
      // console.log(res);
      this.books=[];
      for (const elem of res) {
        this.books.push({ id: 1, title: elem.title, author: elem.url });
        // console.log(elem.title);
      }
      return { axios_data: res };
    },
  },
  async asyncData({ $axios }) {
    // 取得先のURL
    const url = "https://qiita.com/api/v2/items";
    // リクエスト（Get）
    const response = await $axios.$get(url);
    // 配列で返ってくるのでJSONにして返却

    // console.log(response);

    for (const elem of response) {
      console.log(elem.title);
    }

    return {
      posts: response,
    };
  },
};
</script>

<style>
</style>
