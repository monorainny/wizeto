<template>
<div><br><br>

    <div v-for='(c, index) in category' :key='index' >
        <div class='subtitle-1 pl-4'  style='display: block;margin-left: -4px;color: #707070'>
            <v-icon style='font-size: 2rem;margin-left: 5px;'>mdi-menu-right</v-icon>{{c.parent.toUpperCase()}}
        </div>

        <div style='display: flex;flex-wrap: nowrap; overflow-x: auto;'>
            <div v-for='a in c.content' :key='a.id' >
                <div style='width: 230px;height: 350px;flex: 0 0 auto; border: 3px solid #eeeeee;margin-left: 20px; padding: 5px; border-radius: 5px;'>
                    <div v-if='a.image'>
                        <v-img class='mt-1 ml-1' :src="a.image" aspect-ratio="1" alt="" >
                            <template v-slot:placeholder>
                                <v-row class="fill-height ma-0" align="center" justify="center">
                                    <v-progress-circular indeterminate color="grey lighten-5"
                                    ></v-progress-circular>
                                </v-row>
                            </template>
                        </v-img>
                    </div>
                    <div v-else style='line-height: 40px; text-align: center;'>
                        <v-icon>mdi-checkbox-marked-circle-outline</v-icon>
                    </div>

                    <div class='container'>
                        <div>
                            <nuxt-link class='body-2 font-weight-bold' style='text-decoration: none; color: #455a64' :to="'/display/' + a.id" >{{a.name.toUpperCase()}}</nuxt-link>
                        </div>
                        <div class='caption' >{{textCut(a.description, 60)}}</div>
                        <div class='body-2 font-weight-bold'  style='color: #8c9eff;float: right'>${{a.price}}</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    computed:{
        category(){
            return this.$store.state.parent.category
        }
    },
    methods:{
        textCut(txt, len, lastTxt) {
            if (len == "" || len == null) { // 기본값
                len = 20;
            }
            if (lastTxt == "" || lastTxt == null) { // 기본값
                lastTxt = "...";
            }
            if (txt.length > len) {
                txt = txt.substr(0, len) + lastTxt;
            }
            return txt;
        }
    }
}
</script>

<style>

</style>