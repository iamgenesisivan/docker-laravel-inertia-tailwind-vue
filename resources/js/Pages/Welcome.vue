<template>
    <div>
        <Head title="Welcome" />

        <Section class="
            grid
            grid-cols-2
            text-right
            bg-gray-800
            text-gray-300
        ">
            <div>
                <jet-application-mark class="h-12 w-auto"></jet-application-mark>
            </div>
            <div v-if="canLogin">
                <Link v-if="$page.props.user" :href="route('dashboard')" class="text-sm underline">
                    Dashboard
                </Link>

                <template v-else>
                    <Link :href="route('login')" class="text-base underline">
                        Log in
                    </Link>

                    <Link v-if="canRegister" :href="route('register')" class="text-base underline place-self-end ml-4">
                        Register
                    </Link>
                </template>
            </div>
        </Section>

        <Section 
            class="
                bg-gray-800
                pt-16
                h-screen
            "
        >
            <div
                class="h-2/3 flex flex-wrap content-between pb-36"
            >
                <p
                    class="
                        border-b-2
                        font-bold
                        border-gray-400
                        pb-3
                        text-2xl
                        text-gray-300
                        uppercase
    
                    "
                >
                Hey! This is Genesis. I'm a software engineer and I would be glad to work with you.</p>
                <div class="flex items-end border-b-2 border-b-gray-500 pb-2">
                    <p
                        class="
                            font-bold
                            mr-5
                            text-gray-500
                            text-xl
                        "
                    >Want to know more?</p>
                    <jet-button
                        class="
                            bg-green-400
                            font-bold
                            rounded
                            text-sm
                            text-gray-800
                            hover:bg-green-800
                        "
                        @click="contacting = true"
                    >
                        Let's chat
                    </jet-button>
                </div>
            </div>

            <div class="
                animate-pulse mt-3 text-gray-300 text-center text-9xl
            ">
                <a href="#skills">&#8675;</a>
            </div>
        </Section>
        
        <Section id="skills" class="bg-gray-200 text-gray-800 h-screen">
            <h2
                class="
                    text-6xl
                    font-bold
                    pt-3

                "
            >Shitty</h2>
            
            <div class="grid grid-cols-2">
                <div v-for="skill in skills">
                    <Skill :background="skill.color">
                        {{ skill.name }}
                    </Skill>
                </div>
            </div>

            <div class="flex justify-center mt-10">
                <jet-button
                    class="
                        bg-indigo-800
                        font-bold
                        rounded
                        text-sm
                        text-gray-200
                        hover:bg-indigo-700
                    "
                    @click="contacting = true"
                >
                    Get in touch
                </jet-button>
            </div>

        </Section>
        
        <Section class="bg-gray-600 text-gray-200 h-screen">
            <h2
            
            class="
            text-6xl
            font-bold
            pt-3
           "
            >BObo</h2>

            <div v-for="(project, index) in projects">
                <Project :title="project.title" :description="project.description" :color="project.color">

                </Project>

                <!-- <AcademicCapIcon class="size-20">

                </AcademicCapIcon> -->
                <!-- <template v-if="project"> -->
                    <component :is="getIconComponent(project,index)" class="size-20">
    
                    </component>

                <!-- </template> -->
            </div>

            <div class="flex justify-center mt-10">
                <jet-button
                    class="
                        bg-purple-100
                        font-bold
                        rounded
                        text-sm
                        text-gray-800
                        hover:bg-purple-700
                    "
                    @click="contacting = true"
                >
                    Know more
                </jet-button>
            </div>

        </Section>
        
        <Section
            class="
                flex
                justify-between
                bg-gray-800
                text-gray-300
                text-xl
            "
        >
            <p>&copy; iGenesis. All rights reserved.</p>
            <div
                class="
                    flex justify-evenly items-center
                "
            >
                <Link class="border-b pb-1 hover:text-gray-50 px-2" href="">Github</Link>
                <Link class="border-b pb-1 hover:text-gray-50 px-2" href="">Twitter</Link>
                <Link class="border-b pb-1 hover:text-gray-50 px-2" href="">StackOverflow</Link>
            </div>
        </Section>

        <jet-modal :show="contacting" @close="contacting=null">
            <div class="bg-gray-50 shadow-2xl p-8">
                <p class="text-gray-600 text-2xl font-extrabold text-center">Let me know some details.</p>


                <form
                    class="flex flex-col items-center p-16"
                    @submit.prevent="submit"
                >
                    <input
                        class="px-5 py-3 w-96 border border-gray-600 rounded"
                        type="email"
                        name="email"
                        placeholder="Your email"
                    />

                    <!-- <jet-input-error :message="form.errors.email"/> -->

                    <textarea
                        class="px-5 py-3 w-96 border border-gray-600 rounded mt-5"
                        name="message"
                        placeholder="The details :)"
                    ></textarea>

                    <!-- <jet-input-error :message="form.errors.message"/> -->

                    <!-- :disabled="form.processing" -->
                    <jet-button
                        class="px-5 py-3 mt-5 w-96 bg-purple-400 justify-center rounded-xl text-sm"
                    >
                        <!-- <span class="animate-spin mr-1" v-show="form.processing">
                            &#9696;
                        </span> -->

                        <!-- <span v-show="!form.processing"> -->
                            Get in touch
                        <!-- </span> -->
                    </jet-button>
                </form>


            </div>

        </jet-modal>
    </div>
</template>
<script>

import { Head, Link } from '@inertiajs/vue3';
import { defineAsyncComponent, defineComponent } from 'vue';
import JetApplicationMark from '../Components/ApplicationMark.vue'
import JetButton from '../Components/PrimaryButton.vue'
import JetModal from '../Components/Modal.vue'
import Section from '../Components/Childrens/Section.vue'
import Skill from '../Components/Childrens/Skills.vue'
import Project from '../Components/Childrens/Projects.vue'
// import {} from '@heroicons/vue/24/solid'

// import * as heroIcons from '@heroicons/vue/24/solid';
// import {AcademicCapIcon} from '@heroicons/vue/24/solid'
// import Project from '../Components/Childrens/Projects.vue'

    export default defineComponent({
        components: {
            Head,
            Link,
            JetApplicationMark,
            Section,
            JetButton,
            Skill,
            JetModal,
            Project,
            // BeakerIcon,
            // AcademicCapIcon
        },
        props: {
            canLogin: Boolean,
            canRegister: Boolean,
            skills: Object,
            projects: Object,
        },
        data() {
            return {
                contacting: null,
            }
        },
        methods: {
            getIconComponent(item,index) {
                // )
                return defineAsyncComponent(() => {
                    return import('@heroicons/vue/24/solid/AcademicCapIcon')
                    // .then((module) => module.default)
                    .catch((err) => {
                        console.error("Error loading icon:", err);
                        return null; // Handle error if icon fails to load
                    });
                });
            },
        }
    })
</script>


