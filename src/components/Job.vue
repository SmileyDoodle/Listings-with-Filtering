<template>
  <div>
      <div v-for="data in myJson" :key="data.id" class="job-wrap">
        <div class="logo-wrap">
            <img :src="require(`../assets/images/${data.logo}`)" alt="icon">
            <!-- <img :src="getLogo(data.logo)" alt="icon"> -->
        </div>
        <div>
            <div class="company-wrap">
                <p> {{data.company}} </p>
                <p>NEW!</p>
                <p>FEATURED</p>
            </div>
            <div class="title-wrap">
                <h3> {{data.position}} </h3>
            </div>
            <div class="description-wrap">
                <p> {{data.postedAt}} </p>
                <p> {{data.contract}} </p>
                <p> {{data.location}} </p>
            </div>
        </div>
        <div class="skills-wrap">
            <p>Frontend</p>
            <p>Senior</p>
            <p>HTML</p>
            <p>CSS</p>
            <p>Javascreept</p>
        </div>
      </div>
  </div>
</template>

<script>
import json from '../data.json'
console.log(json)

export default {
    name: 'Job',
    data() {
        return{
            myJson: json,
        }
    },
}
</script>

<style>
.job-wrap {
    display: flex;
    background-color: #fff;
    width: 1000px;
    margin: 4rem auto;
}
.job-wrap:last-child {
    margin-bottom: 0;
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
    margin: 2rem 0 0;
}
.title-wrap h3 {
    margin: 0.5rem 0;
    text-align: left;
}
.description-wrap {
    display: flex;
}
.description-wrap p {
    font-size: 0.8rem;
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
</style>