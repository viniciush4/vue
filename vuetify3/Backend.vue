<template id="backend">
    <v-app id="inspire">
        <v-navigation-drawer :clipped="$vuetify.breakpoint.lgAndUp" v-model="drawer" fixed app >
            <v-list dense>
                <template v-for="item in items" >
                    <v-layout v-if="item.heading" :key="item.heading" row align-center >
                        <v-flex xs6>
                            <v-subheader v-if="item.heading">
                                {{ item.heading }}
                            </v-subheader>
                        </v-flex>
                        <v-flex xs6 class="text-xs-center">
                            <a href="#!" class="body-2 black--text">EDIT</a>
                        </v-flex>
                    </v-layout>
                    <v-list-group  v-else-if="item.children" v-model="item.model" :key="item.text" :prepend-icon="item.model ? item.icon : item['icon-alt']" append-icon="" >   
                        <v-list-tile slot="activator" >
                            <v-list-tile-content>
                            <v-list-tile-title>
                                {{ item.text }}
                            </v-list-tile-title>
                            </v-list-tile-content>
                        </v-list-tile>
                        <v-list-tile v-for="(child, i) in item.children" :key="i" @click="" router :to="child.action">
                            <v-list-tile-action v-if="child.icon">
                                <v-icon>{{ child.icon }}</v-icon>
                            </v-list-tile-action>
                            <v-list-tile-content>
                                <v-list-tile-title>
                                    {{ child.text }}
                                </v-list-tile-title>
                            </v-list-tile-content>
                        </v-list-tile>
                    </v-list-group>
                    <v-list-tile v-else :key="item.text" @click="" router :to="item.action">
                        <v-list-tile-action>
                            <v-icon>{{ item.icon }}</v-icon>
                        </v-list-tile-action>
                        <v-list-tile-content>
                            <v-list-tile-title>
                                {{ item.text }}
                            </v-list-tile-title>
                        </v-list-tile-content>
                    </v-list-tile>
                </template>
            </v-list>
        </v-navigation-drawer>
        <v-toolbar :clipped-left="$vuetify.breakpoint.lgAndUp" color="blue darken-3" dark app fixed >
            <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
                <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
                <span class="hidden-sm-and-down">Estoque Bacana</span>
            </v-toolbar-title>
            <v-text-field flat solo-inverted hide-details prepend-inner-icon="search" label="Localizar" class="hidden-sm-and-down" ></v-text-field>
            <v-spacer></v-spacer>
            <v-menu bottom left>
                <v-btn icon slot="activator" dark icon>
                    <v-icon>person</v-icon>
                </v-btn>
    
                <v-list>
                    <v-list-tile v-on:click="logout()">
                        <v-list-tile-title>Sair</v-list-tile-title>
                    </v-list-tile>
                </v-list>
            </v-menu>
        </v-toolbar>
        <v-content>
            <v-container fluid fill-height>   
                <v-layout row wrap>
                    <v-flex xs12>
                        <slot name="content"></slot>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-content>
    </v-app>
</template>

<script>
    export default {
        name: 'Backend',
        data () {
            return {
                dialog: false,
                drawer: null,
                items: [
                    { icon: 'group', text: 'Usuários', action: '/usuarios' },
                    { icon: 'category', text: 'Categoria de Produtos', action: '/categorias-produtos' },
                    { icon: 'change_history', text: 'Produtos', action: '/produtos' },
                    { icon: 'assessment', text: 'Estoque', action: '/estoque' },
                    {
                        icon: 'keyboard_arrow_up',
                        'icon-alt': 'keyboard_arrow_down',
                        text: 'Relatórios',
                        model: false,
                        children: [
                            { text: 'Balanço Geral do Estoque', action: '/balanco-geral-estoque' },
                            { text: 'Balanço Individual por Produto', action: '/balanco-individual-por-produto' }
                        ]
                    }
                ]
            }
        },
        methods: {
            logout() {
                localStorage.removeItem('token');
                this.$router.replace({ path: "/login" });
            }
        }
    }
</script>