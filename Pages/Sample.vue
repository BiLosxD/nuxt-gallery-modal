<template>
    <div id="container" class="about_us facilities book">
        <breadcrumb :isOverlay="false" />
        <section id="top_content">
            <h1 class="header_title">Facilities</h1>
        </section>
        <section id="content">
            <div class="wrapper" v-for="(facility, fac_key) in facilities" :key="fac_key">
                <div class="field_image" v-for="(image, img_key) in facility.images" :key="img_key">
                    <img
                        class="image_responsive"
                        :src="image.imagePath"
                        @click="openGallery(fac_key)"
                    />
                </div>
                <h1 class="field_title">{{ facility.title }}</h1>
            </div>
        </section>
        <gallery ref="gallery" :images="imagesToSend" />
    </div>
</template>

<script>
    import Breadcrumb from '../../components/Breadcrumb'
    import Gallery from '../../components/modals/Gallery'
    export default {
        components: {
            Breadcrumb,
            Gallery
        },
        data() {
            return {
                imagesToSend: null,
                facilities: [
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/1.png',
                                title: 'Sample'
                            },
                            {
                                imagePath: '/images/about-us/facility/2.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'Manual and Socorro Fong Sports Center'
                    },
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/3.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'Anthony & Justa Lee Student Leadership Center'
                    },
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/1.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'DMCAB'
                    },
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/1.png',
                                title: 'Sample'
                            },
                            {
                                imagePath: '/images/about-us/facility/2.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'The Oratory of St. Francis Xavier'
                    },
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/1.png',
                                title: 'Sample'
                            },
                            {
                                imagePath: '/images/about-us/facility/2.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'XSN Primary Building and Gym'
                    },
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/1.png',
                                title: 'Sample'
                            },
                            {
                                imagePath: '/images/about-us/facility/2.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'Ramon S. Ang Highschool Building'
                    },
                    {
                        images: [
                            {
                                imagePath: '/images/about-us/facility/1.png',
                                title: 'Sample'
                            }
                        ],
                        title: 'The Joy of Teaching'
                    }
                ]
            }
        },
        methods: {
            openGallery(fac_key) {
                this.$refs.gallery.opened = true
                this.imagesToSend = this.facilities[fac_key].images
                document.body.classList.add('no_scroll')
            }
        }
    }
</script>
