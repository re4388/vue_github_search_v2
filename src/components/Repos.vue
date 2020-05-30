<template lang='pug'>
  div
    .center.d-flex.m-4
      b-button.m-2(variant='primary', @click='showAllRepo')
        |All
      b-button.m-2(variant='success', @click='showForkedRepo')
        |Forked
      b-button.m-2(variant='info', @click='showNotForkedRepo')
        |Not forked
      b-button.m-2(variant='warning', @click='showRepoByCreatedDate')
        |Order by created
      .d-flex.m-2
        b-form-input(v-model='userId', debounce='500', placeholder='Enter your Github username')
        b-form-input(v-model='searchWords', debounce='500', placeholder='Enter keyword to search')
    div(v-if='validUsername')
      .center.d-flex.flex-wrap(v-if='searchWords')
        ul(v-for='i in filterSearch', :key='i.id')
          li
            a(:href='`${i.html_url}`', target='_blank')
              | {{ i.name }} {{ i.fork?'/ forked':'' }}
      .center.d-flex.flex-wrap(v-if="searchWords === ''")
        ul(v-for='i in repo', :key='i.id')
          li
            a(:href='`${i.html_url}`', target='_blank')
              | {{ i.name }} {{ i.fork?'/ forked':'' }}
    div(v-else='')
      .d-flex.m-5
        strong Loading...
        b-spinner.ml-4
</template>
<script>
import { GET_USER } from "@/store/actions.type";
import { mapGetters } from "vuex";

export default {
  name: "Repos",

  data() {
    return {
      searchWords: "",
      userId: "re4388",
      repo:{},
    };
  },

  created(){
    this.init()
  },

  computed: {
    ...mapGetters(["fetchRepo", 'validUsername']),
    filterSearch() {
      return this.repo.filter(i => i.name.match(this.searchWords));
    },
  },
  watch: {
      userId: async function() {
      await this.$store.dispatch(GET_USER, this.userId);
      this.repo = this.fetchRepo
      // console.log('from watch', this.repo);
    }
  },

  methods: {
    async init(){
      await this.$store.dispatch(GET_USER, this.userId);
      this.repo = this.fetchRepo
    },
    showAllRepo() {
      this.repo = this.fetchRepo
    },
    showRepoByCreatedDate() {
      this.repo = this.fetchRepo.sort(function(a, b) {
        return new Date(b.created_at) - new Date(a.created_at);
      });
    },
    showForkedRepo() {
      this.repo = this.fetchRepo.filter(i => {
        return i.fork === true;
      });
    },
    showNotForkedRepo() {
      this.repo = this.fetchRepo.filter(i => {
        return i.fork === false;
      });
    }
  }
};
</script>

<style scoped>
ol,
ul {
  list-style: none;
}

/* .news p {
  font-size: 10px;
} */
</style>
