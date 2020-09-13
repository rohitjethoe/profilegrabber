<template>
    <div class="profile">
        <div class="profile-info">
            <div class="profile-pic">
                <img v-bind:src="data.graphql.user.profile_pic_url_hd" alt="">
            </div>
            <div class="profile-data">
                <div class="profile-data-username">
                    {{ data.graphql.user.username }}
                </div>
                <div class="profile-data-stats">
                    <span>
                        <strong>{{ data.graphql.user.edge_owner_to_timeline_media.count }}</strong> 
                        posts
                    </span>
                    <span>
                        <strong>{{ data.graphql.user.edge_followed_by.count }}</strong>
                        followers
                    </span>
                    <span>
                        <strong>{{ data.graphql.user.edge_follow.count }}</strong>
                        following
                    </span>
                </div>
                <div class="profile-data-details">
                    <span>
                        <strong>{{ data.graphql.user.full_name }}</strong>
                    </span> 
                    <br>
                    <span>
                        {{ data.graphql.user.biography }}       
                    </span>
                    <br>
                    <span class="profile-data-details-website" v-if="data.graphql.user.external_url != null">
                        <a :href="data.graphql.user.external_url" target="_blank">
                            {{ data.graphql.user.external_url }}
                        </a>
                    </span>
                </div>
            </div>
        </div>
        <div class="profile-nav">
            <a v-bind:class="{ active : isActive }" v-on:click="isActive = true">Pictures</a>
            <a v-bind:class="{ active : !isActive }" v-on:click="isActive = false">Posts</a>
        </div>
        <div class="profile-pic-download" v-if="isActive">
            <div class="profile-pic-download-image">
                <a v-bind:href="data.graphql.user.profile_pic_url_hd" target="_blank">
                    <img v-bind:src="data.graphql.user.profile_pic_url_hd" alt="profile picture">
                </a>
            </div>
            <div class="profile-pic-downloads">
                <div class="profile-pic-download-button">
                    <a v-bind:href="data.graphql.user.profile_pic_url_hd" target="_blank" class="btn">
                        Download <span><i class="fas fa-arrow-down"></i></span>
                    </a>
                </div>
                <div class="profile-pic-download-img">
                    or click the picture to download.
                </div>
            </div>
        </div>
        <div class="profile-pic-posts" v-if="!isActive">
            <div class="profile-pic-posts-download">
                Click on any picture you want to download.
            </div>
            <div class="profile-pic-posts-post" v-bind:key="item" v-for="item in data.graphql.user.edge_owner_to_timeline_media.edges">
                <a class="profile-pic-post-url" v-bind:href="item.node.display_url" target="_blank">    
                    <img class="profile-pic-post" v-bind:src="item.node.display_url">
                </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Profile",
    props: ['data'],
    data() {
        return {
            isActive: true
        }
    }
}
</script>

<style scoped>
    .profile {
        margin-top: 10%;
    }

    .profile-info {
        display: flex;
        justify-content: space-evenly;
        align-items: center;
        border-bottom: 2px solid #c3c3c3;
        width: 90%;
        margin: 0 auto;
        padding: 20px 0px;
    }

    .profile .profile-pic img {
        border-radius: 100%;
        width: 200px;
    }

    .profile-data-stats {
        font-family: "Roboto", sans-serif;
        margin-top: 10px;
    }

    .profile-data-stats span {
        margin-right: 10px;
    }

    .profile-data-details {
        font-family: "Roboto", sans-serif;
        margin-top: 20px;
    }

    .profile-data-username {
        font-size: 32px;
    }

    .profile-data-details-website a:link, a:visited{
        color: #00376B;
        text-decoration: none;
    }


    @media only screen and (min-width: 629px) {
        .profile-info {
            width: 600px;
        }
    }

    @media only screen and (max-width: 620px) {
        .profile .profile-pic img {
            width: 150px;
        }

        .profile-data-username {
            font-size: 28px;
        }

        .profile-data-details {
            font-size: 14px;
        }

        .profile-data-stats {
            font-size: 14px;
        }
    }

    @media only screen and (max-width: 586px) {

        .profile-data {
            margin-left: 20px;
        }

    }

    @media only screen and (max-width: 472px) {
        .profile-data-username {
            font-size: 20px;
        }

        .profile-data-details {
            font-size: 12px;
            margin-top: 10px;
        }
        .profile-data-stats {
            margin-top: 10px;
            font-size: 12px;
            display: none;
        }
    }

    .profile-nav a {
        color: #c3c3c3;
        text-decoration: none;
        border-top: 2px solid #c3c3c3;
        padding-left: 15px;
        padding-right: 15px;
    }

    .profile-nav a:hover {
        cursor: pointer;
        color: #9b9b9b;
        border-top: 2px solid #9b9b9b;
    }

    .profile-nav .active {
        color: #283747;
        border-top: 2px solid #283747;
    }

    .profile-nav .active:hover {
        color: #283747;
        border-top: 2px solid #283747;
    }

    .profile-nav {
        text-align: center;
    }

    .profile-pic-download-image img {
        width: 160px;
        border-radius: 10px;
        box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.125);
        transition: 0.4s all;
    }

    .profile-pic-download-image img:hover {
        opacity: 0.8;
    }

    .profile-pic-download-button a:link, .profile-pic-download-button a:visited {
        background-color: #275EFE;
        padding-left: 12.5px;
        padding-top: 8px;
        padding-bottom: 8px;
        border-radius: 5px;
        color: #fff;
        text-decoration: none;
    }

    .btn span {
        padding: 7.5px 12.5px;
        border-top-right-radius: 5px;
        border-bottom-right-radius: 5px;
        margin-left: 10px;
        color: #fff;
        background-color: #184FEE;
    }

    .profile-pic-download-img {
        margin-top: 10px;
    }

    .profile-pic-download {
        margin-top: 40px;
    }

    .profile-pic-download-image {
        float: left;
    }

    .profile-pic-downloads {
        float: right;
        margin-top: 50px;
    }

    .profile-pic-download {
        width: 400px;
        margin: 40px auto;
    }

    .profile-pic-download::after {
        clear: both;
        content: "";
        display: table;
    }

    @media only screen and (max-width: 435px) {
        .profile-pic-download-image img {
            width: 130px;
        }
        .profile-pic-download {
            width: 290px;
        }
        .profile-pic-downloads {
            margin-top: 40px;
        }
        .btn {
            font-size: 12px;
        }
        .btn span {
            font-size: 12px;
        }
        .profile-pic-download-img {
            font-size: 12px;
        }
    }    

    .profile-pic-post {
        width: 100%;
        margin-bottom: 25px;
        margin-top: 25px;
        border-radius: 10px;
        transition: 0.4s all;
    }

    .profile-pic-post:hover {
        opacity: 0.8;
    }

    .profile-pic-posts-post {
        margin: 0 auto;
        width: 300px;
    }

    @media only screen and (max-width: 350px) {
        .profile-pic-posts-post {
            width: 250px;
        }
    }

    .profile-pic-posts-download {
        text-align: center;
        margin-top: 30px;
    }

    .profile {
        min-height: calc(100vh - 61px - 28px);
    }
</style>