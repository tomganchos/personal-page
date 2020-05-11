<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <header>
      <h1 class="header-name">Artem Kriuchkov</h1>
      <ul class="experience-list">
        <li v-for="item in experience" :key="item.description" class="experience-item" @click="openNewWindow(item.link)">
          <span class="experience-item__title">{{ item.title }}</span>
          <span class="experience-item__description">{{ item.description }}</span>
        </li>
      </ul>
      <div class="header-education">
        <h2 class="education-title">Education</h2>
        <ul class="education-list">
          <li v-for="item in education" :key="item.description" class="education-item" @click="openNewWindow(item.link)">
            <span class="education-item__title">{{ item.title }}</span>
            <span class="education-item__description">{{ item.description }}</span>
          </li>
        </ul>
      </div>
      <div class="header-avatar">
        <avatar-component/>
      </div>
      <ul class="link-list">
        <link-component v-for="(item, index) in links"
                        :key="item.icon"
                        :icon="item.icon"
                        :link="item.link"
                        :description="item.description"
                        :data-index="index"
                        class="link-item"/>
      </ul>
    </header>
    <div class="divider"/>
    <main>
      <project-component v-for="(item, index) in projects" :key="item.name" :data-index="index"/>
    </main>
  </div>
</template>

<script>
  import { gsap } from "gsap"

  import LinkComponent from "@/components/linkComponent"
  import AvatarComponent from "@/components/AvatarComponent"
  import ProjectComponent from "@/components/projectComponent"

export default {
  name: 'App',
  components: {
    ProjectComponent,
    AvatarComponent,
    LinkComponent
  },
  data () {
    return {

      experience: [
        {
          title: 'Front-end developer - OOO "Aeronavigator"',
          description: 'Jul 2017 - Present',
          link: 'http://aeronavigator.ru'
        }
      ],
      education: [
        {
          title: 'Saint Petersburg Electrotechnical University "LETI"',
          description: '2016 - 2018, Master’s degree, Software Engineering',
          link: 'https://etu.ru/'
        },
        {
          title: 'The Bonch-Bruevich Saint-Petersburg State University of Telecommunications',
          description: '2012 - 2016, Bachelor’s degree, Software Engineering',
          link: 'https://www.sut.ru/'
        }
      ],
      links: [
        {
          link: 'https://github.com/tomganchos',
          description: 'github.com/tomganchos',
          icon: 'github'
        },
        {
          link: 'https://www.linkedin.com/in/kriuchkov-art',
          description: 'linkedin.com/in/kriuchkov-art',
          icon: 'linkedin'
        },
        {
          link: 'https://www.instagram.com/kriuchkov_art',
          description: 'instagram.com/kriuchkov_art',
          icon: 'instagram'
        },
        {
          link: 'https://vk.com/kriuchkov_art',
          description: 'vk.com/kriuchkov_art',
          icon: 'vk'
        },
        {
          link: 'https://steamcommunity.com/id/tomganchos',
          description: 'steamcommunity.com/id/tomganchos',
          icon: 'steam'
        },
      ],
      projects: [
        {
          name: 'gameLife',
          description: 'Conway\'s Game of Life',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        }
      ]
    }
  },
  mounted () {
    gsap.from('.header-name', {opacity: 0, duration: 0.5, y: -20})
    let delay = 0.1
    gsap.from('.experience-list', {opacity: 0, duration: 0.5, delay: delay, y: -20})
    delay += 0.1
    gsap.from('.header-education', {opacity: 0, duration: 0.5, delay: delay, y: -20})
    delay += 0.1
    gsap.from('.header-avatar', {opacity: 0, duration: 0.5, delay: delay, y: -20})
    delay += 0.1
    this.links.forEach((project, index) => {
      gsap.from('.link-item[data-index="' + index + '"]', {opacity: 0, duration: 0.5, delay: delay, y: -20})
      delay += 0.1
    })
    gsap.from('.divider', {opacity: 0, duration: 0.5, delay: delay, y: -20})
    delay += 0.1
    this.projects.forEach((project, index) => {
      console.log(index)
      gsap.from('.project[data-index="' + index + '"]', {opacity: 0, duration: 0.5, delay: delay, y: -20})
      delay += 0.1
    })
  },
  methods: {
    openNewWindow (link) {
      let otherWindow = window.open();
      otherWindow.opener = null;
      otherWindow.location = link;
    }
  }
}
</script>

<style>
  #app {
    font-family: Roboto, Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  header {
    max-width: 1200px;
    display: grid;
    grid-template-columns: 400px 400px 400px;
    grid-template-rows: 60px auto auto;
    margin-top: 5em;
  }
  .header-name {
    font-weight: normal;
    font-size: 2em;
    margin: 0 0 0.25em 0;
    justify-self: end;
  }
  .experience-list {
    grid-column: 1;
    grid-row: 2;
    margin: 0;
    padding: 0;
    justify-self: end;
    list-style: none;
  }
  .experience-item {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    padding-bottom: 0.7em;
  }
  .experience-item:hover {
    color: darkcyan;
    cursor: pointer;
  }
  .experience-item:last-child {
    padding-bottom: 0;
  }
  .experience-item__title {
    padding-bottom: 0.2em;
    text-align: right;
  }
  .experience-item__description {
    color: #999;
    font-size: 0.9em;
    text-align: right;
  }
  .experience-item:hover .experience-item__description {
    color: darkcyan;
  }
  .header-education {
    grid-column: 1;
    grid-row: 3;
    align-self: flex-end;
  }
  .education-title {
    display: flex;
    margin: 0;
    justify-content: flex-end;
    font-size: 0.8em;
    color: #999;
    font-weight: normal;
    margin-bottom: 0.3em;
  }
  .education-list {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .education-item {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    margin-bottom: 0.7em;
  }
  .education-item:last-child {
    margin-bottom: 0;
  }
  .education-item:hover {
    color: darkcyan;
    cursor: pointer;
  }
  .education-item__title {
    padding-bottom: 0.2em;
    text-align: right;
  }
  .education-item__description {
    text-align: right;
    color: #999;
    font-size: 0.9em;
  }
  .education-item:hover .education-item__description {
    color: darkcyan;
  }
  .header-avatar {
    grid-column: 2;
    grid-row: 1 / 4;
    height: 300px;
    width: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .link-list {
    grid-column: 3;
    grid-row: 2 / 4;
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .link-item {
    display: flex;
    align-items: center;
    padding: 10px 0;
  }
  .link-item:hover {
    color: darkcyan;
    cursor: pointer;
  }
  /*>>>.link-item path:hover {*/
  /*  fill: red !important;*/
  /*  display: none;*/
  /*}*/
  .link-item:first-child {
    padding-top: 0;
  }
  .link-item:last-child {
    padding-bottom: 0;
  }
  .divider {
    margin: 50px 0;
    width: 1200px;
    height: 4px;
    background-color: #B4D6D3;
    border-radius: 50%;
  }
  main {
    display: grid;
    grid-template-columns: 300px 300px 300px;
    grid-template-rows: 200px 200px 200px;
    grid-gap: 50px;
  }
</style>
