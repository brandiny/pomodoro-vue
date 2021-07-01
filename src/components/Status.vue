<template>
  <div id="status">
      <div @click="handleClickWork" :class="{work : isWork}">Work</div>
      <div @click="handleClickBreak" :class="{break : isBreak}">Break</div>
  </div>
</template>

<script>
export default {
    emits: ["work", "break"],
    props: {
        status: String
    },

    methods: {
        handleClickWork() {
            this.$emit('work')
        },

        handleClickBreak() {
            this.$emit('break')
        }
    },

    computed: {
        isBreak: function() {
            return this.status === "break";
        },

        isWork: function() {
            return this.status === "work";
        }
    }
}
</script>

<style>
#status {
    max-width: 500px;
    height: 60px;

    margin: auto;
    margin-top: 2em;
    border-radius: 10px;
    display: flex;
    align-items: stretch;
    justify-content: stretch;
    cursor: pointer;
}

#status div {
    flex: 1;
    color: rgba(255, 255, 255, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5em;
    font-weight: bold;
    letter-spacing: 1px;
    background: #ccc;
    
}

#status div:hover {
    opacity: 0.8;
}

#status div:nth-child(1) {
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
}


#status div:nth-child(2) {
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
}

</style>