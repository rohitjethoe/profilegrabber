<template>
    <div class="search">
        <form>    
            <input class="search-bar" v-model="query" type="text" v-on:change="fetchAccount" placeholder="Search here..." v-on:keydown.enter="fetchAccount"> 
        </form>
    </div>    
</template>

<script>
export default {
    name: "Search",
    data() {
        return {
            query: ""
        }
    },
    methods: {
        fetchAccount(e) {
            e.preventDefault();
            fetch(`//www.instagram.com/${this.query}?__a=1`)
            .then(res => {
                return res.json();
            }).then(this.setResults);
        },

        setResults(results) {
            if (results.graphql === undefined) {
                this.query = "";
            } else {
                this.$emit("query", results);
            }
        },
    }
}
</script>

<style scoped>
    .search {
        display: flex;
        justify-content: center;
        margin-top: 20%;
    }

    .search input {
        border: none;
        border-bottom: 3px solid rgba(215, 219, 221, 0.5);
        font-size: 42px;
        padding-bottom: 15px;
        color: #d7dbdd;
        width: 400px;
        transition: 0.5s all;
        border-radius: 0px;
    }

    .search input:focus {
        border: none;
        border-bottom: 3px solid rgb(40, 55, 71, 0.5);
        color: rgba(40, 55, 71);
        outline: 0;
    }

    .false-username {
        color: #a50606;
    }

    @media only screen and (max-width: 600px) {
        .search input {
            font-size: 32px;
            width: 320px;
        }
    }

    @media only screen and (max-width: 370px) {
        .search input {
            font-size: 24px;
            width: 240px;
        }
    }

    @media only screen and (max-width: 250px) {
        .search input {
            font-size: 18px;
            width: 80%;
        }
    }

    .search {
        min-height: calc(100vh - 161px - 28px);
    }
</style>