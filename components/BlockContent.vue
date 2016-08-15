<template>
    <h1>Teste</h1>
    <div class="row">
        <button class="act-add-block btn btn-primary" @click="addBlock($event)">Adicionar Bloco</button>
        <button class="btn btn-success">Salvar</button>
    </div>
    <hr>
    <div class="row container-blocks">
        <div class="col-md-6" v-for="list in BlockContentList">
            <br>
            <input type="text" v-model="list.title" class="form-control" value="{{ list.title }}" />
            <p v-show="!list.title" class="text-danger">O titulo deve ser preenchido</p>
            <br>
            <textarea class="editor1 form-control" cols="30" rows="10">
                {{ list.content }}
            </textarea>
        </div>
    </div>
</template>

<script>
// Insira a linha abaixo dentro da tag script na pagina onde será exibido o CKEDITOR, deverá estar acima do chamada do CKEDITOR
//     var CKEDITOR_BASEPATH = '/node_modules/ckeditor/';
import $ from 'jquery'
import {} from 'ckeditor'
console.log(CKEDITOR);

export default {
    data: function() {
        return {
            BlockContentList: [{
                id: 1,
                title: 'Quem Somos',
                content: 'Lorem Ipsum é simplesmente uma simulação de texto da indústria tipográfica e de impressos, e vem sendo utilizado desde o século XVI, quando um impressor desconhecido pegou uma bandeja de tipos e os embaralhou para fazer um livro de modelos de tipos.',
                validate: {
                    required: true,
                    minlength: 8
                }
            }, {
                id: 2,
                title: 'Saiba Mais',
                content: 'É um fato conhecido de todos que um leitor se distrairá com o conteúdo de texto legível de uma página quando estiver examinando sua diagramação.',
                validate: {
                    required: true,
                    maxlength: 16
                }
            }]
        }
    },
    methods: {
        addBlock: function(e) {
            var self = this;
            this.BlockContentList.unshift({
                title: 'Novo Bloco',
                content: ''
            });
            setTimeout(function() {
                self.loadEditor($('.editor1')[0]);
            }, 100);
        },
        loadEditor: function(el = null) {
            var self = this;
            if (el == null) {
                var textarea = $('.editor1');
                $.each(textarea, function(key, value) {
                    self.changeEditor(value);
                });
            } else {
                self.changeEditor(el);
            }
        },
        changeEditor: function(el) {
            CKEDITOR.replace(el);
        },
        validationTitle: function() {
            alert('foi');
        }
    },
    ready: function() {
        this.loadEditor();
    }
};
</script>

<style lang="stylus" scoped>
h1
    color red
</style>
