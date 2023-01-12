<template>
    <transition>
        <Modal
                :y="linkClientY"
                v-if="linkIsCopied">
        </Modal>
    </transition>
    <Tooltip
            v-show="visible"
            @visible="setVisible"
            :x="coords.x"
            :y="coords.y"
    >
    </Tooltip>
    <span class="main">
        <div class="lineNumberSpace">
            <span v-for="(number, index) in linesNumber"
                  @click="selectNumber(index)"
                  :class="{active: (index === selectedNumber)}"
                  class="numbers">
                <div v-if="number.toString().length > 1">{{number}}</div>
                <div v-else="number.toString().length === 1">&nbsp;{{number}}</div>
            </span>
        </div>
        <h1 ref="h1" @click="setZIndex">
            <div ref="lines" class="lines">
                <div class="line"
                     v-for="(number, index) in linesNumber"
                     :class="{activeLine: (index === selectedNumber)}"
                ></div>
            </div>
            <p>
                <span class="green">const </span>
                <i><span class="gray">CV </span></i>
                <span class="symbols">= {</span>
            </p>
            <br>
            {{tab}}<p>
            <span class="keys">name</span>
            <span class="symbols">: </span>
            <span class="text">'Ceretean Rodion'</span>
            <span class="commas">,</span>
        </p>
            <br>
            <div style="display: inline-block"
                 @mouseover="showExperienceTooltip"
                 @mouseleave="hideExperienceTooltip">
                <p>{{tab}}<span class="keys">experience</span>
                <span class="symbols">: {</span>
                <br>
                {{tab}}{{tab}}<span class="keys">job</span>
                <span class="symbols">: </span>
                <span class="text">'freelance'</span>
                <span class="commas">,</span>
                <br>
                {{tab}}{{tab}}<span class="keys">date</span>
                <span class="symbols">: {</span>
                <br>
                {{tab}}{{tab}}{{tab}}<span class="keys">since</span>
                <span class="symbols">: </span>
                <span class="text">'January 2022'</span>
                <span class="commas">,</span>
                <br>
                {{tab}}{{tab}}{{tab}}<span class="keys">to</span>
                <span class="symbols">: </span>
                <span class="text">'present'</span>
                <span class="commas">,</span>
                <br>
                {{tab}}{{tab}}<span class="symbols">}</span>
                <br>
                {{tab}}<span class="symbols">}</span>
                <span class="commas">,</span>
            </p></div>
            <br>
            {{tab}}<p>
            <span class="keys">phone</span>
            <span class="symbols">: </span>
            <span class="text">'+37367142299'</span>
            <span class="commas">,</span>
        </p>
            <br>
            {{tab}}<p>
            <span class="keys">email</span>
            <span class="symbols">: </span>
            <span class="text">'ceretean.r@gmail.com'</span>
            <span class="commas">,</span>
        </p>
            <br>
            {{tab}}<p>
            <span class="keys">skills</span>
            <span class="symbols">: </span>
            <span v-if="isArrayOpen && media < 1050"
                  @click="closeArray">
            <span class="symbols">[</span>
                <br>
            {{tab}}{{tab}}<span class="text">'javascript'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'typescript'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'git'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'Vue3'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'Nuxt JS'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'HTML5'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'SCSS'</span>
                <br>
            {{tab}}<span class="symbols">]</span>
                </span>
            <span class="symbols"
                  v-if="media < 1050 && !isArrayOpen"
                  @click="openArray">
                [...]
            </span>
            <span v-else-if="media >= 1050">
            <span class="symbols">[</span>
            <span class="text">'javascript'<span class="commas">,</span>
                    'typescript'<span class="commas">,</span>
                    'git'<span class="commas">,</span>
                    'Vue3'<span class="commas">,</span>
                    'Nuxt JS'<span class="commas">,</span>
                    'HTML5'<span class="commas">,</span>
                    'SCSS'</span>
            <span class="symbols">]</span>
                </span>
           <span class="commas">,</span>
        </p>
            <br>
            <p v-if="isLanguageArrayOpen && media < 650" @click="closeLanguageArray">
                {{tab}}<span class="keys">languages</span>
                <span class="symbols">: </span>
                <span class="symbols">[</span>
                <br>
                {{tab}}{{tab}}<span class="text">'Russian'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'English'<span class="commas">,</span>
                <br>
                    {{tab}}{{tab}}'Romanian'</span>
                <br>
                {{tab}}<span class="symbols">]</span>
                <span class="commas">,</span>
            </p>
            <p v-if="media < 650 && !isLanguageArrayOpen">
                {{tab}}<span class="keys">languages</span>
                <span class="symbols">: </span>
                <span @click="openLanguageArray" class="symbols">[...]</span>
                <span class="commas">,</span>
            </p>
            {{tab}}<p v-if="media >= 650">
            <span class="keys">languages</span>
            <span class="symbols">: </span>
            <span class="symbols">[</span>
            <span class="text">'Russian'<span class="commas">,</span>
                    'English'<span class="commas">,</span>
                    'Romanian'</span>
            <span class="symbols">]</span>
            <span class="commas">,</span>
        </p>
            <br>
            {{tab}}<p>
            <span class="keys">github</span>
            <span class="symbols">: </span>
            <span class="text" v-if="media >= 850">'https://github.com/RodionCeretean'</span>
            <span class="text link" v-else
                  @click="copyToClipboard('https://github.com/RodionCeretean', $event)">link</span>
            <span class="commas">,</span>
        </p>
            <br>
            {{tab}}<p>
            <span class="keys">linkedIn</span>
            <span class="symbols">: </span>
            <span class="text" v-if="media >= 850">'https://www.linkedin.com/in/rodion-ceretean/'</span>
            <span class="text link" v-else
                  @click="copyToClipboard('https://www.linkedin.com/in/rodion-ceretean/', $event)">link</span>
        </p>
            <br>
            <p>
                <span ref="last" class="symbols">}</span>
            </p>
        </h1>
    </span>
</template>

<script>
    import Tooltip from './tooltip.vue'
    import Modal from './Modal.vue'

    export default {
        name: "MainPage",
        components: {Tooltip, Modal},
        mounted() {
            this.totalHeight = document.documentElement.offsetHeight
            window.addEventListener('resize', this.setMedia)
        },
        updated() {
            this.totalHeight = this.$refs.last.getBoundingClientRect().bottom + window.pageYOffset
        },
        data() {
            return {
                linkClientY: null,
                linkIsCopied: false,
                isLanguageArrayOpen: false,
                isArrayOpen: false,
                media: document.documentElement.clientWidth,
                selectedNumber: null,
                totalHeight: null,
                visible: false,
                coords: {
                    x: null,
                    y: null
                }
            }
        },
        methods: {
            copyToClipboard(url, event) {
                this.linkClientY = event.clientY
                navigator.clipboard.writeText(url)
                this.linkIsCopied = true
                setTimeout(() => {
                    this.linkIsCopied = false
                }, 1500)
            },
            openLanguageArray() {
                this.isLanguageArrayOpen = true
            },
            closeLanguageArray() {
                this.isLanguageArrayOpen = false
            },
            closeArray() {
                this.isArrayOpen = false
            },
            openArray() {
                this.isArrayOpen = true
            },
            setMedia() {
                this.media = document.documentElement.clientWidth
            },
            setVisible() {
                this.visible = true
            },
            hideExperienceTooltip() {
                this.visible = false
            },
            showExperienceTooltip(event) {
                this.visible = true
                this.coords.x = event.pageX
                this.coords.y = event.pageY
            },
            selectNumber(index) {
                this.selectedNumber = index
                this.$refs.lines.style.zIndex = '1'
                this.$refs.h1.style.webkitUserSelect = 'none'
                setTimeout(() => this.$refs.h1.style.webkitUserSelect = 'text', 1)
            },
            setZIndex() {
                this.$refs.lines.style.zIndex = '-1'
            }
        },
        computed: {
            tab() {
                if (this.media < 450) {
                    return '\xa0'
                }
                return '\xa0\xa0\xa0\xa0'
            },
            linesNumber() {
                if (this.totalHeight / 63.5 % 0) {
                    return this.totalHeight / 63.5
                } else {
                    return Math.ceil(this.totalHeight / 63.5)
                }
            },
        }
    }
</script>

<style scoped lang="scss">

    .main {
        background-color: #2b2b2b;
        height: content-box;
        display: flex;
        min-height: 100vh;
        width: 100%;

        h1 {
            color: green;
            margin-left: 15px;
            margin-top: 5px;
            font-family: monospace;
            line-height: 1.975;
            font-size: 2rem;
            min-width: content-box;
            width: 100%;
            overflow: hidden;
            position: relative;
            @media screen and (max-width: 1650px) {
                font-size: 1.75rem;
                line-height: 2.25;
            }
            @media screen and (max-width: 1450px) {
                font-size: 1.5rem;
                line-height: 2.625;
            }
            @media screen and (max-width: 1250px) {
                font-size: 1.25rem;
                line-height: 3.15;
            }
            @media screen and (max-width: 450px) {
                font-size: 1rem;
                line-height: 3.95;
            }
            @media screen and (max-width: 350px) {
                font-size: 0.9rem;
                line-height: 4.39;
            }

            &::selection {
                background: #214283;
            }

            br::selection {
                background: #214283;
            }
        }

        .lines {
            width: 100%;
            height: 100%;
            position: absolute;
            left: 0;
            top: 0;
            z-index: -1;

            .line {
                width: 100%;
                height: 63.5px;
            }
        }

        p {
            display: inline;
            white-space: nowrap;

            &::selection {
                background: #214283;
            }

            .green {
                color: #2BCC0B;

                &::selection {
                    background: #214283;
                }
            }

            .gray {
                color: #CCBE52;

                &::selection {
                    background: #214283 !important;
                }
            }

            .symbols {
                color: #A9B7C6;

                &::selection {
                    background: #214283;
                }
            }

            .keys {
                color: #FF8B87;

                &::selection {
                    background: #214283;
                }
            }

            .text {
                color: #6A8759;

                &::selection {
                    background: #214283;
                }
            }

            .link {
                text-decoration: underline;
                cursor: pointer;
            }

            .commas {
                color: #CC7832;

                &::selection {
                    background: #214283;
                }
            }
        }
    }

    .lineNumberSpace {
        min-width: fit-content;
        padding: 0 10px;
        display: flex;
        flex-direction: column;
        background-color: #313335;
        width: 10%;
        height: content-box;
        line-height: 2;
        font-size: 1.5rem;
        text-align: end;

        .numbers {
            margin-top: 15px;
            margin-right: 75%;
            color: #606366;
            font-family: monospace;
            cursor: default;
            -webkit-user-select: none;
        }
    }

    .active {
        color: #A4A3A3 !important;
    }

    .activeLine {
        background-color: #606366;
        opacity: 0.5;
    }

    .v-enter-active,
    .v-leave-active {
        transition: opacity 1s ease-in;
    }

    .v-enter-from,
    .v-leave-to {
        opacity: 0;
    }

    .v-enter-to,
    .v-leave-from {
        opacity: 1;
    }
</style>