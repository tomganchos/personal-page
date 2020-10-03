<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <header>
      <h1 class="header-name">Artem Kriuchkov</h1>
      <ul class="experience-list">
        <li v-for="(item, index) in experience"
            :key="item.description"
            :ref="'experience-item-' + index"
            class="experience-item"
            @click="openNewWindow(item.link)"
            @mouseover="onMouseOver('experience-item-' + index)"
            @mouseleave="onMouseLeave('experience-item-' + index)">
          <span class="experience-item__title">{{ item.title }}</span>
          <span class="experience-item__description">{{ item.description }}</span>
        </li>
      </ul>
      <div class="header-education">
        <h2 class="education-title">Education</h2>
        <ul class="education-list">
          <li v-for="(item, index) in education"
              :key="item.description"
              :ref="'education-item-' + index"
              class="education-item"
              @click="openNewWindow(item.link)"
              @mouseover="onMouseOver('education-item-' + index)"
              @mouseleave="onMouseLeave('education-item-' + index)">
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
                        :ref="item.icon"
                        :icon="item.icon"
                        :link="item.link"
                        :description="item.description"
                        :data-index="index"
                        class="link-item"
                        @mouseover="onMouseOver(item.icon)"
                        @mouseleave="onMouseLeave(item.icon)"/>
      </ul>
    </header>
    <div class="divider" ref="divider"/>
    <main>
      <project-component v-for="(item, index) in projects"
                         :key="item.name"
                         :project="item"
                         :data-index="index"
                         :project-index="index"
                         :ref="'project-' + index"
                         class="project"
                         @mouseover="onMouseOver"
                         @mouseleave="onMouseLeave"/>
    </main>
  </div>
</template>

<script>
  import { gsap } from "gsap"

  import LinkComponent from "@/components/linkComponent"
  import AvatarComponent from "@/components/AvatarComponent"
  import ProjectComponent from "@/components/ProjectComponent"

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
          icon: 'github',
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
          name: 'Tourism site',
          description: 'Site of Pskov children\'s tourism center',
          tags: ['Vue', 'vuex', 'vue-router', 'axios', 'vue-google-adsense', 'vue-yandex-maps', 'moment'],
          img: 'project-tourism-site.png',
          link: 'http://turizmpskov.ru/'
        },
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
          name: 'tourismSite1',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite2',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite3',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite4',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        },
        {
          name: 'tourismSite5',
          description: 'Site of Pskov child tourism',
          tags: ['Vue', 'css'],
          img: ''
        }
      ],
      themeColor: null,
      themeColorsList: [
        'turquoise', 'lemon', 'tomato', 'violet', 'lime'
      ],
      themeColors: {
        turquoise: {
          strong: '#48D1CC',
          weak: 'rgba(175,238,238,0.3)'
        },
        lemon: {
          strong: '#F0E68C',
          weak: 'rgba(255,250,205,0.3)'
        },
        tomato: {
          strong: '#FF6347',
          weak: 'rgba(255,160,122,0.3)'
        },
        violet: {
          strong: '#DDA0DD',
          weak: 'rgba(216,191,216,0.3)'
        },
        lime: {
          strong: '#00FF7F',
          weak: 'rgba(152,251,152,0.3)'
        }
      }
    }
  },
  created () {

  },
  mounted () {
    this.setFirstThemeColor()
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
      gsap.from('.project[project-index="' + index + '"]', {opacity: 0, duration: 0.5, delay: delay, y: -20})
      delay += 0.1
    })
    this.setThemeColor()
    console.log(this.$refs)
  },
  methods: {
    openNewWindow (link) {
      let otherWindow = window.open();
      otherWindow.opener = null;
      otherWindow.location = link;
    },
    setFirstThemeColor () {
      this.themeColor = this.themeColorsList[Math.floor(Math.random() * this.themeColorsList.length)]
      gsap.to('#app', {backgroundImage: 'linear-gradient(to bottom, ' +  this.themeColors[this.themeColor].weak + ' 0%, #FFFFFF 50%)' })
      gsap.to('.experience-item:hover', {color: this.themeColors[this.themeColor].strong})
      gsap.to('.education-item:hover', {color: this.themeColors[this.themeColor].strong})
      gsap.to('.divider', {backgroundColor: this.themeColors[this.themeColor].strong})
      gsap.to('.project', {backgroundColor: this.themeColors[this.themeColor].weak})
      gsap.to('.header-avatar ellipse.border', {stroke: this.themeColors[this.themeColor].strong, fill: this.themeColors[this.themeColor].weak})
    },
    setThemeColor () {
      setInterval(() => {
        let themeColor = this.themeColorsList[Math.floor(Math.random() * this.themeColorsList.length)]
        gsap.to('#app', {backgroundImage: 'linear-gradient(to bottom, ' + this.themeColors[themeColor].weak + ' 0%, #FFFFFF 50%)', duration: 10 })

        // gsap.to('.experience-item:hover', {color: this.themeColors[themeColor].strong, duration: 10})
        // gsap.to('.education-item:hover', {color: this.themeColors[themeColor].strong, duration: 10})
        gsap.to('.divider', {backgroundColor: this.themeColors[themeColor].strong, duration: 10})
        gsap.to('.project', {backgroundColor: this.themeColors[themeColor].weak, duration: 10})
        gsap.to('.header-avatar ellipse.border', {stroke: this.themeColors[themeColor].strong, fill: this.themeColors[themeColor].weak, duration: 10})
      }, 10000)
    },
    onMouseOver (ref) {
      const color = this.$refs.divider.style.backgroundColor
      if (this.$refs[ref][0].$el && this.$refs[ref][0].$el.classList.contains('project')) {
        this.$refs[ref][0].$el.querySelector('.project-name').style.color = color
      } else if (this.$refs[ref][0].$el) {
        this.$refs[ref][0].$el.style.color = color
        this.$refs[ref][0].$el.querySelector('svg .color').style.fill = color
      } else {
        this.$refs[ref][0].style.color = color
        this.$refs[ref][0].lastChild.style.color = color
      }
    },
    onMouseLeave (ref) {
      if (this.$refs[ref][0].$el && this.$refs[ref][0].$el.classList.contains('project')) {
        this.$refs[ref][0].$el.querySelector('.project-name').style.color = '#000'
      } else if (this.$refs[ref][0].$el) {
        this.$refs[ref][0].$el.style.color = '#000'
        this.$refs[ref][0].$el.querySelector('svg .color').style = ''
      } else {
        this.$refs[ref][0].style.color = '#000'
        this.$refs[ref][0].lastChild.style.color = '#888'
      }
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
    background: linear-gradient(180deg, #b4d6d335 0%, #FFFFFF 50%);
    transition: background 1000ms linear;
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
    color: #888;
    font-size: 0.9em;
    text-align: right;
  }
  .header-education {
    grid-column: 1;
    grid-row: 3;
    align-self: flex-end;
  }
  .education-title {
    display: flex;
    margin: 0 0 0.3em 0;
    justify-content: flex-end;
    font-size: 0.8em;
    color: #888;
    font-weight: normal;
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
    cursor: pointer;
  }
  .education-item__title {
    padding-bottom: 0.2em;
    text-align: right;
  }
  .education-item__description {
    text-align: right;
    color: #888;
    font-size: 0.9em;
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
    /*background-color: #B4D6D3;*/
    border-radius: 50%;
  }
  main {
    display: grid;
    grid-template-columns: 300px 300px 300px;
    grid-template-rows: 200px 200px 200px;
    grid-gap: 50px;
  }
  main >>> .project .project-name:hover {

  }
</style>
