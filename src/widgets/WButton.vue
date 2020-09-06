<template>
    
        <a v-if="href" :href="href" :class="extraClass" :disabled="disabled">
            <slot />
        </a>
        <router-link v-else-if="to" :to='to' :class="extraClass" :disabled="disabled">
            <slot />
        </router-link>        
        <button v-else :type="type" :class="extraClass" :event="event" :disabled="disabled" @click="eventHandler">
            <slot />
        </button>        
      
</template>

<script>
export default {
    name: 'WButton',
    props: {
      event: {
        type: String,
        default: 'click'
      },
        href: {
            type: String,
            required: false
        },
        type: {
            type: String,
            required: false
        },
        to: {
            type: String,
            required: false
        },
        size: {
            type: String,
            required: true
        },
        color: {
            type: String,
            required: true
        },
        disabled: {
            type: Boolean,
            required: false
        }
    },
    computed: {
        extraClass () {
            let classes = ['btn']
            if (this.color === 'dark') {
                classes.push('dark-btn')
            } else if (this.color === 'light') {
                classes.push('light-btn')
            }

            if (this.size === 'sm') {
                classes.push('sm-btn')
            } else if (this.size === 'md') {
                classes.push('md-btn')
            }   else if (this.size === 'lg') {
                classes.push('lg-btn')
            }
            return classes
        }
    },
    methods: {
      eventHandler() {
        this.$emit(this.event)
      }
    }    
}
</script>

<style lang="scss">

 .btn {
    padding: 5px 20px;   
    border-radius: 5px;
    outline: none;
    line-height: 24px;
    transition: 0.3s;
    cursor: pointer;
    border: 2px solid #111B47;
    display: inline-block;
 }

 .dark-btn {
    background: #111B47;    
    color: #fff;
    &:hover {
        background: transparent;
        border: 2px solid #111B47;
        color: #111B47;
    }    
 }
 .light-btn {
    background: transparent;
    color: #111B47;
    &:hover {
        background: #111B47;
        border: 2px solid #111B47;
        color: #fff;
    }    
}
    .sm-btn {        
        font-size: 1.4em;
    }
    .md-btn { 
        padding: 6px 30px;        
        font-size: 1.2em;
    }
    .lg-btn { 
        padding: 7px 40px;       
        font-size: 16px;
    }
</style>    