<template>
    <div class="mx-auto bg-white shadow rounded-lg max-w-sm overflow-hidden">
        <timezone-item
        v-for="(timezone, key) in convertedTimezones"
        :timezone="timezone"
        @remove="onRemove"
        >
        </timezone-item>
        <timezone-form 
        v-model="selectedCity"
        :addTimezone="addTimezone"
        :cities="cities"
        @add="addTimezone = true"
        @cancel="addTimezone = false"
        >
        </timezone-form>
    </div>
</template>

<script>
import TimezoneItem from './TimezoneItem'
import TimezoneForm from './TimezoneForm'
import MomentTimezone from 'moment-timezone'
const localTimezone = MomentTimezone.tz.guess()

export default {
    components: {
        TimezoneItem,
        TimezoneForm
    },
    data () {
        return {
            timezones: [],
            timezoneOptions: [],
            addTimezone: false,
            localTimezone: '',
            selectedCity: ''
        }
    },
    async created () {
        await this.getTimezones()

        this.localTimezone = this.timezoneOptions.find(value => {
            return value.timezones.find(timezone => timezone === localTimezone)
        })

        this.timezones = localStorage.getItem('timezones') ? JSON.parse(localStorage.getItem('timezones')) : []

        if (!this.timezones.length) {
            this.timezones.push(this.localTimezone)
        }
    },
    computed: {
        convertedTimezones () {
            return this.timezones.map(value => {
                return {
                    timezone: value.capital,
                    time: MomentTimezone.tz(value.timezones[0]).format('h:mm A').split(' ')
                }
            })
        },
        cities () {
            return this.timezoneOptions
                .filter(value => value.capital)
                .map(value => {
                    return value.capital
                })
        }
    },
    watch: {
        selectedCity () {
            this.timezones.push(
                this.timezoneOptions.find(value => value.capital === this.selectedCity)
            )
        },
        timezones () {
            localStorage.setItem('timezones', JSON.stringify(this.timezones))
        }
    },
    methods: {
        async getTimezones () {
            await fetch('https://api.myjson.com/bins/dukeu')
            .then(response => response.json())
            .then(data => {
                this.timezoneOptions = data
            })
        },
        onRemove (timezone) {
            this.timezones = this.timezones.filter(value => value.capital !== timezone.timezone)
        }
    }
}
</script>

