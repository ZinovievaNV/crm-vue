<template>
  <ul class="sidenav app-sidenav open">
    <router-link class="waves-effect waves-orange pointer"></router-link>

    <router-link
      v-for="link in links"
      :key="link.url"
      tag="li"
      active-class="active"
      :to="link.url"
  
    >
      <a href="#" class="waves-effect waves-orange pointer">{{
        link.title
      }}</a>
    </router-link>
  </ul>
</template>

<script>
export default {
  //оборачивает в круглые скобки,так как мы не можем сразу писать объект
  data: () => ({
    links: [
      { title: 'Счет', url: '/' },
      { title: 'История', url: '/history' },
      { title: 'Планирование', url: '/planning' },
      { title: 'Новая запись', url: 'record' },
      { title: 'Категории', url: '/categories' },
    ],
  }),
  // data() {
  //   return {
  //     links: [
  //       {title: 'Счет',url:'/'},
  //       {title: 'История',url:'/history'},
  //       {title: 'Планирование',url:'/planning'},
  //       {title: 'Новая запись',url:'record'},
  //       {title: 'Категории',url:'/categories'},
  //       ],
  //   };
  // },
};
</script>