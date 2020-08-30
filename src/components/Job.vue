<template>
  <div>
      <div class="filter-wrap">
          <div class="btn-wrap">
            <div v-for="filter in filters" :key="filter">
                <p class="btn-top">{{filter}}</p>
                <button><img src="../assets/images/clear.svg" alt="clear"></button>
            </div>
          </div>
          <button class="btn-clear" @click="clear()">Clear</button>
      </div>
      <div v-for="data in myJson" :key="data.id" class="job-wrap" :class="{ special: data.featured }">
        <div class="logo-wrap">
            <img :src="require(`../assets/images/${data.logo}`)" alt="icon">
            <!-- <img :src="getLogo(data.logo)" alt="icon"> -->
        </div>
        <div>
            <div class="company-wrap">
                <p> {{data.company}} </p>
                <p v-if="data.new">NEW!</p>
                <p v-if="data.featured">FEATURED</p>
            </div>
            <div class="title-wrap">
                <h3> {{data.position}} </h3>
            </div>
            <div class="description-wrap">
                <p> {{data.postedAt}} </p>
                <p>•</p>
                <p> {{data.contract}} </p>
                <p>•</p>
                <p> {{data.location}} </p>
            </div>
        </div>
        <div class="skills-wrap">
            <button class="btn-filter" @click="onSelect(data.role)" > {{data.role}} </button>
            <button class="btn-filter" @click="onSelect(data.level)" > {{data.level}} </button>
            <button v-for="language in data.languages" :key="language" class="btn-filter" @click="onSelect(language)" > {{language}} </button>
            <button v-for="tool in data.tools" :key="tool" class="btn-filter" @click="onSelect(tool)"> {{tool}} </button>
        </div>
      </div>
  </div>
</template>

<script>
import json from '../data.json'
// import { filter } from 'vue/types/umd'
console.log(json)

export default {
    name: 'Job',
    data() {
        return{
            myJson: json,
            filters: []
        }
    },
    methods: {
        onSelect(filter) {
            this.filters.push(filter)
            console.log(this.filters)
        },
        clear() {
            this.filters = []
        }
    }
}
</script>

<style>
.filter-wrap {
    position: relative;
    top: -34px;
    margin-left: auto;
    margin-right: auto;
    left: 0;
    right: 0;
    align-items: center;
    display: flex;
    justify-content: space-between;
    background-color: #fff;
    width: 1000px;
    min-height: 4.5rem;
    margin: 0 auto;
    border-radius: 5px;
}
.filter-wrap p {
    padding: 0;
    margin: 0;
}
.btn-wrap {
    display: flex;
}
.btn-top {
    height: fit-content;
    font-weight: 700;
    padding: 0.3rem;
    border-radius: 5px;
    background-color: hsl(180, 31%, 95%);
    border-color:  hsl(180, 31%, 95%);
    color: hsl(180, 29%, 50%);
    margin-right: 1rem;
}
.btn-top:first-child {
    margin-left: 2rem;
}
.btn-clear {
    margin-right: 1rem;
}
.job-wrap {
    display: flex;
    background-color: #fff;
    width: 1000px;
    margin: 4rem auto;
    border-radius: 5px;
}
.job-wrap:last-child {
    margin-bottom: 0;
}
.special {
    border-left-style: solid;
    border-color: hsl(180, 29%, 50%);
}
.logo-wrap {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 2rem;
}
.logo-wrap img {
    height: 5.5rem;
}
.company-wrap {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
}
.company-wrap p {
    font-size: 0.8rem;
    font-weight: 700;
    color: hsl(180, 29%, 50%);
    margin: 2rem 0 0;
}
.title-wrap h3 {
    margin: 0.5rem 0;
    text-align: left;
}
.title-wrap h3:hover {
    cursor: pointer;
    color: hsl(180, 29%, 50%);
}
.description-wrap {
    display: flex;
}
.description-wrap p {
    font-size: 0.8rem;
    color: hsl(180, 8%, 52%);
    margin: 0 0 2rem;
    padding-right: 0.8rem;
}
.skills-wrap {
    display: flex;
    flex: 1;
    align-items: center;
    justify-content: flex-end;
}
.skills-wrap p {
    font-size: 0.8rem;
    margin: 0;
    padding-right: 0.8rem;
}
.skills-wrap p:last-child {
    padding-right: 2.5rem;
}
.btn-filter {
    font-weight: 700;
    padding: 0.3rem;
    border-radius: 5px;
    background-color: hsl(180, 31%, 95%);
    border-color:  hsl(180, 31%, 95%);
    color: hsl(180, 29%, 50%);
    margin-right: 1rem;
}
</style>