
<!-- fetch APIを使用した場合 -->

<script setup>
import { ref } from 'vue';
const books = ref([]);

const fetchBooks = async () => {
  const response = await fetch('http://localhost:4000', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({
      query: `query{
               books{
                title
                author
               }
            }`,
    }),
  });
  const { data } = await response.json();
  console.log('data', data)
  books.value = data.books;
};


fetchBooks();

</script>

<template>
  <h1>Fetchを利用したGraphQLへのアクセス</h1>
  <ul>
    <li v-for="(book, index) in books" :key="index">
      {{ book.title }}/{{ book.author }}
    </li>
  </ul>
</template>

<!-- apollo-composableを使用した場合(うまくいかないので保留) -->

<!-- <script setup>
import { useQuery } from '@vue/apollo-composable';
import gql from 'graphql-tag';

const { result } = useQuery(gql`
  query {
    books {
      title
    }
  }
`);
</script>

<template>
  <h1>Fetchを利用したGraphQLへのアクセス</h1>
  <ul v-if="result && result.books">
    <li> v-for="(book, index) in result.books" :key="index">
      {{ book.title }}/{{ book.author }}
    </li>
  </ul>
</template> -->


