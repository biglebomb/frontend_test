<template>
    <v-container>
        <div class="headline text-uppercase text-center my-5">program unggulan</div>

        <v-spacer></v-spacer>

        <v-row justify="space-around">

            <v-chip-group
                    mandatory
                    active-class="primary"
                    v-model="selectedTag"
                    @change="onTagChanges"
            >
                <v-chip color="default" v-for="tag in tags" :key="tag">
                    {{ tag[0] + tag.substring(1).toLowerCase() }}
                </v-chip>
            </v-chip-group>
        </v-row>

        <v-spacer></v-spacer>

        <v-row>
            <v-col cols="12" lg="8" md="10" offset-lg="2" offset-md="1">
                <v-container>
                    <v-row>
                        <v-col cols="12" lg="4" md="6" sm="6" v-for="item in getPrograms()" :key="item.id" class="d-flex">
                            <v-hover v-slot:default="{ hover }">
                                <v-card
                                        :elevation="hover ? 7 : 0"
                                        class="d-flex flex-column"
                                        outlined
                                        tile
                                >
                                    <v-img
                                            class="white--text align-end"
                                            height="200px"
                                            :src="item.avatar"
                                    >
<!--                                        <v-overlay-->
<!--                                                :absolute="true"-->
<!--                                                :value="!!hover"-->
<!--                                        >-->
<!--                                            Lihat yuk-->
<!--                                        </v-overlay>-->
                                    </v-img>
                                    <v-card-title class="mb-2">{{item.name}}</v-card-title>

                                    <v-card-subtitle class="pb-0 mb-2">
                                        <div v-if="item.price > 1 || item.price_normal > 1">
                                            <div style="text-decoration: line-through;">Rp.{{formatPrice(item.price_normal)}}</div>
                                            <div class="headline green--text align-center">Rp.{{formatPrice(item.price)}}
                                                <v-chip
                                                        class="ma-2 mt-0"
                                                        color="red"
                                                        text-color="white"
                                                        small
                                                >
                                                    -{{100-(100/(item.price_normal/item.price))}}%
                                                </v-chip>
                                            </div>
                                        </div>
                                        <div v-else>
                                            <div class="headline green--text">Gratis</div>
                                        </div>
                                    </v-card-subtitle>

                                    <v-card-text class="text--primary flex-grow-1">
                                        {{item.abstract}}
                                    </v-card-text>

                                    <v-divider class="mx-1"></v-divider>

                                    <v-card-actions>
                                        <v-btn
                                                color="primary"
                                                text
                                        >
                                            Lihat lebih lanjut
                                        </v-btn>
                                    </v-card-actions>
                                </v-card>
                            </v-hover>
                        </v-col>
                    </v-row>
                </v-container>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
    import programs from '../assets/programs.json'

    export default {
        name: "Landing",

        data: () => ({
            programs: {},
            tags: [
                'All',
                'UJIANMU',
                'KELASMU',
                'KARIERMU'
            ],
            selectedTag: 0,
            features: [
                {title: "Tanyamu", description: "Tanyakan latihan soal atau tugas rumah yang sulit kepada guru dan temanmu dari berbagai daerah.", color: ''},
                {title: "Ujianmu", description: "Pemahaman belajar yang lebih terstruktur untuk menghadapi berbagai ujian pendidikan."},
                {title: "Kelasmu", description: "Jadi lebih kompeten melalui program blended learning yang menyenangkan bersama siswa sekolah lain."},
                {title: "Kariermu", description: "Program magang bersertifikasi di perusahaan dan interaksi langsung dengan para pakar."},
            ]

        }),
        created() {
            this.programs = programs.data
        },
        methods: {
            onTagChanges() {
                console.log(this.selectedTag)
                if (this.selectedTag !== 0)
                    this.programs = programs.data.filter(item => {
                        return item.category_name === this.tags[this.selectedTag]
                    })
                else
                    this.programs = programs.data
            },
            formatPrice(value) {
                let val = (value/1).toFixed(2).replace('.', ',')
                return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
            },
            getPrograms(){
                return this.programs.filter(item => {
                    return item.status === true;
                })
            }
        }
    };
</script>

<style scoped>
    .v-responsive {
        flex: unset;
    }
</style>
