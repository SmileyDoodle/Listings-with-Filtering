<template>
  <div class="box">
      <!-- Hidden element -->
      <div class="filter-container">
        <div class="filter-wrap" v-show="isSeen">
            <div class="btn-wrap">
                <div class="btn-box" v-for="(filter, index) in filters" :key="filter">
                    <p class="btn-top">{{filter}}</p>
                    <button class="btn-remove" @click="remove(index)"><img src="../assets/images/clear.svg" alt="clear"></button>
                </div>
            </div>
            <button class="btn-clear" @click="clear()">Clear</button>
        </div>
      </div>
      <!-- Listing -->
      <div v-for="data in myJson" :key="data.id" >
        <div class="job-wrap" :class="{ special: data.featured }" v-if="checkExist(data)">
            <div class="logo-wrap">
                <img :src="require(`../assets/images/${data.logo}`)" alt="icon">
            </div>
            <div class="main-info-wrap">
                <div class="company-wrap">
                    <p> {{data.company}} </p>
                    <p class="new-wrap" v-if="data.new">NEW!</p>
                    <p class="featured-wrap" v-if="data.featured">FEATURED</p>
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
            filters: [],
            isSeen: false
        }
    },
    methods: {
        onSelect(filter) {
            this.isSeen = true;
            let item = filter;
                if (this.filters.includes(item) === false) {
                    this.filters.push(item);
                    console.log("item", item);
                    console.log(this.filters);
                } else {
                    console.log("err")
                }    
        },
        remove(index) {
            this.filters.splice(index, 1);
            if (this.filters.length < 1) {
                this.isSeen = false;
            } else {
                this.isSeen = true;
            }
        },
        clear() {
            this.isSeen = false;
            this.filters = []
        },
        checkExist(data) {
            const arr = [...data.languages, ...data.tools];
            arr.push(data.level);
            arr.push(data.role);
            var lowerCaseArray = [];
            for (var i = 0; i < arr.length; i++) {
                lowerCaseArray.push(arr[i].toLowerCase());
            }

            let checker = (arr, target) => target.every(v => arr.includes(v.toLowerCase()));
            if(this.filters.length > 0) {
                return checker(lowerCaseArray, this.filters);
            } else {
                return true;
            }
        }
    },
}
</script>

<style>
.filter-container {
    position: relative;
    top: -38px;
    min-height: 4.7rem;
}
.filter-wrap {
    position: relative;
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
    box-shadow: 0px 10px 14px -7px #cde2e6;
}
.filter-wrap p {
    padding: 0;
    margin: 0;
}
.btn-wrap {
    display: flex;
}
.btn-wrap:first-child {
    margin-left: 2.5rem;
}
.btn-box {
    display: flex;
    align-items: center;
    margin-right: 1rem;
}
.btn-top {
    font-size: 0.8rem;
    height: fit-content;
    font-weight: 700;
    padding: 0.3rem !important;
    border-top-left-radius: 5px;
    border-bottom-left-radius: 5px;
    background-color: hsl(180, 31%, 95%);
    border-color:  hsl(180, 31%, 95%);
    color: hsl(180, 29%, 50%);
	cursor:pointer;
	text-decoration: none;
    border: 2px solid hsl(180, 31%, 95%);
}
.btn-remove {
    background-color: hsl(180, 29%, 50%);
    border-color:  hsl(180, 29%, 50%);
    border-top-right-radius: 5px;
    border-bottom-right-radius: 5px;
    cursor: pointer;
	text-decoration: none;
    border: 2px solid hsl(180, 29%, 50%);
}
.btn-remove:hover {
    background-color: #000;
    border: 2px solid #000;
}
.btn-clear {
    color: #000;
    background-color: transparent;
    border: none;
    font-weight: 700;
    margin-right: 2.5rem;
    text-decoration: underline;
    cursor:pointer;
}
.btn-clear:hover {
    color: hsl(180, 29%, 50%);
}
.job-wrap {
    display: flex;
    background-color: #fff;
    width: 1000px;
    height: 160px;
    margin: 1.5rem auto;
    border-radius: 5px;
    box-shadow: 0px 10px 14px -7px #cde2e6;
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
.main-info-wrap {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: left;
}
.company-wrap {
    display: flex;
    align-items: center;
}
.company-wrap p {
    font-size: 0.8rem;
    font-weight: 700;
    color: hsl(180, 29%, 50%);
    margin-right: 1rem;
}
.new-wrap {
    font-size: 0.6rem !important;
    color: #fff !important;
    background-color: hsl(180, 29%, 50%);
    padding: 8px 9px;
    border-radius: 15px;
}
.featured-wrap {
    font-size: 0.6rem !important;
    color: #fff !important;
    background-color: #000;
    padding: 8px 9px;
    border-radius: 15px;
}
.title-wrap h3 {
    margin: 0.3rem 0;
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
    /* margin: 0 0 2rem; */
    padding-right: 0.8rem;
}
.skills-wrap {
    display: flex;
    flex: 1;
    align-items: center;
    justify-content: flex-end;
}
.btn-filter {
    font-weight: 700;
	cursor:pointer;
    padding: 0.3rem;
	text-decoration: none;
    border-radius: 5px;
    background-color: hsl(180, 31%, 95%);
    border-color:  hsl(180, 31%, 95%);
    color: hsl(180, 29%, 50%);
    margin-right: 1rem;
    border: 2px solid hsl(180, 31%, 95%);
}
.btn-filter:last-child {
    margin-right: 2.5rem;
}
.btn-filter:hover {
    background-color: hsl(180, 29%, 50%);
    color: #fff;
}
button:focus {
    outline-color: transparent;
}
</style>