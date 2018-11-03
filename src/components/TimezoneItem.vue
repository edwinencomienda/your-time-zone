<template>
<div class="border-b-1 border-grey-light p-8 flex items-center justify-between relative" v-if="timezone">
    <svg @click="remove" class="fill-current w-2 absolute pin-t pin-r mr-4 mt-4 cursor-pointer text-grey-dark hover:text-grey-darker" aria-hidden="true" data-prefix="fas" data-icon="times" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 352 512">
        <path class="fill-current" d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"></path>
    </svg>
    <div class="text-2xl text-grey-darkest">{{ timezone.timezone }}</div>
    <div class="text-left mr-2">
        <div class="text-4xl relative">
            <span class="mr-6">{{ timezone.time[0] }}</span> 
            <span class="text-sm text-grey-dark absolute pin-y pin-r">{{ timezone.time[1] }}</span>
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: ['timezone'],
    methods: {
        remove () {
            this.$emit('remove', this.timezone)
        }
    }
}
</script>
