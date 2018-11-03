<template>
<div class="text-grey hover:text-grey-darkest cursor-pointer flex">
    <div v-if="addTimezone" class="flex flex-1">
        <select @change="onChange" class="p-4 outline-none bg-grey-lighter flex-1">
            <option value="">Select City</option>
            <option v-for="city in cities" :value="city">{{ city }}</option>
        </select>
        <div @click="cancel" class="p-4 cursor-pointer">
            Cancel
        </div>
    </div>
    <div v-else class="flex-1 p-4 text-center" @click="add">
        <svg class="w-6" aria-hidden="true" data-prefix="fas" data-icon="plus" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
            <path class="fill-current" d="M416 208H272V64c0-17.67-14.33-32-32-32h-32c-17.67 0-32 14.33-32 32v144H32c-17.67 0-32 14.33-32 32v32c0 17.67 14.33 32 32 32h144v144c0 17.67 14.33 32 32 32h32c17.67 0 32-14.33 32-32V304h144c17.67 0 32-14.33 32-32v-32c0-17.67-14.33-32-32-32z"></path>
        </svg>
    </div>
</div>
</template>

<script>
export default {
    props: {
        addTimezone: {
            type: Boolean,
            required: true
        },
        cities: {
            type: Array,
            required: false,
            default: () => []
        }
    },
    methods: {
        add () {
            this.$emit('add')
        },
        cancel () {
            this.$emit('cancel')
        },
        onChange (e) {
            this.$emit('input', e.target.value)
            this.cancel()
        }
    }
}
</script>

