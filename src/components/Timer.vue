<template>
  <div @click="$emit('stop')" :class="{break : isBreak, work : isWork}" id="timer">
    <h1>
        <slot name="minutes"></slot>:<slot name="seconds"></slot>
    </h1>
  </div>
</template>

<script>
export default {
    props: {
        status: String,
        running: Boolean
    },

    computed: {
        isBreak: function() {
            return this.status === "break" && this.running;
        },

        isWork: function() {
            return this.status === "work" && this.running;
        }
    },
}
</script>

<style>
#timer {
    max-width: 420px;
    height: 200px;
    margin: auto;
    border-radius: 3em;
    padding: 0px;
    color: white;
    background: #aaa;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3em;

    /* transition: 0.5s all; */
}

#timer:hover {
    opacity: 0.8;
    cursor: pointer;
}

#timer > * {
    margin: 0;
    padding: 0;
    transition: none;
}

.work {
    background: crimson !important;
}

.break {
    background: #3CDC14 !important;
}
</style>