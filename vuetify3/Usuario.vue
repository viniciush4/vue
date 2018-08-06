<template id="usuarios">
    <backend>
        <template slot="content">
            <v-card width="100%">
                <v-toolbar flat color="white">
                    <v-toolbar-title>Usuários</v-toolbar-title>
                    <v-spacer></v-spacer>
                    <v-dialog v-model="dialog" max-width="500px">
                        <v-btn slot="activator" color="primary" dark class="mb-2">Novo Usuário</v-btn>
                        <v-card>
                            <v-card-title>
                                <span class="headline">{{ formTitle }}</span>
                            </v-card-title>
                    
                            <v-card-text>
                                <v-container grid-list-md>
                                    <v-form ref="form" v-model="valid" lazy-validation>
                                        <v-layout row wrap>
                                            <v-flex xs12>
                                                <v-text-field prepend-icon="person" v-model="editedItem.nome" label="Nome" :rules="rules.nome"></v-text-field>
                                            </v-flex>
                                        </v-layout>
                                        <v-layout row wrap>
                                            <v-flex xs12>
                                                <v-text-field v-model="editedItem.login" label="Login" :rules="rules.login"></v-text-field>
                                            </v-flex>
                                        </v-layout>
                                        <v-layout row wrap>
                                            <v-flex xs12>
                                                <v-text-field v-model="editedItem.senha" label="Senha" :rules="rules.senha"></v-text-field>
                                            </v-flex>
                                        </v-layout>
                                        <v-layout row wrap>
                                            <v-flex xs12>
                                                <v-select v-model="editedItem.tipo" :items="tiposUsuarios" label="Tipo" :rules="rules.tipo"></v-select>
                                            </v-flex>
                                        </v-layout>
                                    </v-form>
                                </v-container>
                            </v-card-text>
                    
                            <v-card-actions>
                                <v-spacer></v-spacer>
                                <v-btn color="blue darken-1" flat @click.native="close">Cancelar</v-btn>
                                <v-btn color="blue darken-1" flat @click.native="save" :disabled="!valid">Salvar</v-btn>
                            </v-card-actions>
                        </v-card>
                    </v-dialog>
                </v-toolbar>
                <v-toolbar flat color="white">
                    <v-text-field v-model="search" append-icon="search" label="Localizar" single-line hide-details></v-text-field>
                </v-toolbar>
                <v-data-table :headers="headers" :items="usuarios" hide-actions class="elevation-1" :search="search" >
                    <template slot="items" slot-scope="props">
                        <td>{{ props.item.nome }}</td>
                        <td class="text-xs-right">{{ props.item.login }}</td>
                        <td class="text-xs-right">{{ props.item.tipo }}</td>
                        <td class="justify-end layout">
                            <v-icon small class="mr-2" @click="editItem(props.item)" >edit</v-icon>
                            <v-icon small @click="deleteItem(props.item)">delete</v-icon>
                        </td>
                    </template>
                    <template slot="no-data">
                        Nenhum dado disponível
                    </template>
                </v-data-table>
            </v-card>
        </template>
    </backend>
</template>



<script>

</script>