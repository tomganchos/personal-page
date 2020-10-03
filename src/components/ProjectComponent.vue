<template>
  <div>
    <img :src="project.img" alt="project image">
    <div class="project-text">
      <div class="project-name"
           @click="openNewWindow(project.link)"
           @mouseover="$emit('mouseover', 'project-' + dataIndex)"
           @mouseleave="$emit('mouseleave', 'project-' + dataIndex)">{{ project.name }}</div>
      <div class="project-description">{{ project.description }}</div>
      <div class="project-tags">
        <span class="tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "ProjectComponent",
    props: ['project', 'color', 'dataIndex'],
    methods: {
      openNewWindow (link) {
        // console.log(this.color)
        console.log(link)
        let otherWindow = window.open()
        otherWindow.opener = null
        otherWindow.location = link
      }
    }
  }
</script>

<style scoped>
  .project {
    background-color: #D7FDF0;
    border-radius: 20px;
    position: relative;
  }
  .project .project-text {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 20px;
  }
  .project img {
    width: 300px;
    opacity: 0.1;
    border-radius: 20px;
  }
  .project .project-name {
    font-size: 1.5em;
    margin-bottom: 4px;
    cursor: pointer;
    text-decoration: underline;
  }
  .project .project-name:hover {
    color: #888;
  }
  .project .project-description {
    margin-bottom: 4px;
  }
  .project .project-tags {
    display: flex;
    flex-flow: wrap;
    color: #888;
  }
  .project .tag {
    margin-right: 4px;
    font-size: 0.9em;
    white-space: nowrap;
  }
</style>
