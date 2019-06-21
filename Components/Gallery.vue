<template>
    <div :class="`gallery_modal ${(opened) ? 'opened' : ''} ${(toggled) ? 'toggled' : ''}`">
        <div class="main">
            <div class="overlay">
                <button type="button" class="left_arrow" @click="prev()"></button>
                <div :class="`main_image ${(key == activeThumb) ? 'slide_out' : ''}`" v-for="(data, key) in images" :key="key" v-if="key == activeThumb">
                    <h2 id="main_title" class="image_title">{{ data.title }}</h2>
                    <img id="main_image" class="image_responsive" :src="data.imagePath" />
                </div>
                <button type="button" class="right_arrow" @click="next()"></button>
            </div>
            <div class="controls">
                <button type="button" class="control_toggle" @click="toggler()"></button>
                <button type="button" class="control_close" @click="close()"></button>
            </div>
        </div>
        <div class="thumb">
            <div class="wrapper">
                <div :class="`thumb_image ${(key == 0) ? 'active' : ''}`" v-for="(data, key) in images" :key="key">
                    <img :src="data.imagePath" @click="getThumb(key)" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            images: {
                type: Array,
                default: function () {
                    return [
                        {
                            imagePath: '/images/about-us/facility/1.png',
                            title: 'Sample'
                        },
                        {
                            imagePath: '/images/about-us/facility/2.png',
                            title: 'Sample'
                        }
                    ]
                }
            }
        },
        data () {
            return {
                activeThumb: 0,
                opened: false,
                toggled: false
            }
        },
        methods: {
            toggler () {
                this.toggled ^= true
            },
            close () {
                this.opened = false
                this.toggled = false
                document.body.classList.remove('no_scroll')
            },
            removeSlideAnim () {
                setTimeout( () => {
                    let mainParent = document.querySelector('.main .main_image')
                    mainParent.classList.remove('slide_out')
                }, 300)
            },
            next () {
                let me = this
                let thumbs = document.querySelectorAll('.thumb .thumb_image')
                let thumbKey = me.activeThumb + 1
                let length = me.images.length
                if (thumbKey != length) {
                    me.images.forEach((image, key) => {
                        if (thumbKey == key) {
                            me.activeThumb = key
                            thumbs[key].classList.add('active')
                        } else {
                            thumbs[key].classList.remove('active')
                        }
                    })
                } else {
                    me.activeThumb = 0
                    thumbs.forEach((thumb, index) => {
                        if (me.activeThumb == index) {
                            thumb.classList.add('active')
                        } else {
                            thumb.classList.remove('active')
                        }
                    })
                }
            },
            prev () {
                let me = this
                let thumbs = document.querySelectorAll('.thumb .thumb_image')
                let thumbKey = me.activeThumb - 1
                let length = me.images.length
                if (thumbKey < 0) {
                    me.activeThumb = length - 1
                    thumbs.forEach((thumb, index) => {
                        if (me.activeThumb == index) {
                            thumb.classList.add('active')
                        } else {
                            thumb.classList.remove('active')
                        }
                    })
                } else {
                    me.images.forEach((image, key) => {
                        if (thumbKey == key) {
                            me.activeThumb = key
                            thumbs[key].classList.add('active')
                        } else {
                            thumbs[key].classList.remove('active')
                        }
                    })
                }
            },
            getThumb (key) {
                let me = this
                let thumbs = document.querySelectorAll('.thumb .thumb_image')
                let mainParent = document.querySelector('.main .main_image')
                document.querySelector('.main #main_title').innerHTML = me.images[key].title
                document.querySelector('.main #main_image').src = me.images[key].imagePath
                thumbs.forEach((thumb, index) => {
                    if (key == index) {
                        thumb.classList.add('active')
                    } else {
                        thumb.classList.remove('active')
                    }
                })
                mainParent.classList.add('slide_out')
                this.removeSlideAnim()
            }
        }
    }
</script>
