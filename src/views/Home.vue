<template>
    <div>
        <layout>
            <template v-slot:viewContainer>
                <div class="min-w-screen flex flex-col items-center justify-center px-5 py-5">
                    <topic v-for="infoTopic in infosTopic" 
                        :key="infoTopic.postId" 
                        :userId="infoTopic.id" 
                        :username="infoTopic.username" 
                        :title="infoTopic.title" 
                        :content="infoTopic.content" 
                        :createdAt="infoTopic.createdAt" 
                        :likes="Number(infoTopic.Likes)" 
                        :dislikes="Number(infoTopic.Dislikes)" 
                        :myLike="infoTopic.myLike" 
                        :myDislike="infoTopic.myDislike" 
                        :comments="infoTopic.CommentsNb" 
                        :profilePictureURL="infoTopic.pictureURL" 
                        :topicId="infoTopic.postId"
                        :roleName="infoTopic.roleName"></topic>
                </div>
            </template>
        </layout>
    </div>
</template>

<script>
import layout from '@/components/layout/layout.vue'
import axios from 'axios'
import topic from '@/components/topics/topic.vue'

export default {
    name: 'Home',
    components: {
        layout,
        topic
    },
    data() {
        return {
            infosTopic: []
        }
        },
    methods: { 
        
    },
    created() {
        const token = localStorage.getItem('token');
        const id = localStorage.getItem('id');
        const idTokenKeyValue = id+":"+token;
        axios({
            method: 'get',
            url: 'http://localhost:3000/api/posts',
            headers: {
                'Authorization': `Basic ${idTokenKeyValue}` 
            }
        })
        .then(reponse => {
            this.infosTopic = reponse.data;
            console.log(this.infosTopic);
        })
        .catch(error => {
            console.log(error);
        })
    }
}
</script>