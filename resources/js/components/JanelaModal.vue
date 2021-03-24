<template>
    <div>
        <div id="myModal" class="modal-win">
             <div class="modal-content">
                <div class="modal-header">
                    <h2>{{myHeader}}</h2>
                    <span class="close" @click="closeClick">×</span>
                </div>
                <div class="modal-body">
                    <p>
                        <slot>Coloque aqui o texto de sua Janela Modal.</slot>
                    </p>
                </div>
                <div class="modal-footer">
                    <h3>{{myFooter}}</h3>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        //Fecha o modal quando usuário clicar no X
        closeClick() {
            myModal.style.display = "none";
        },
        //Fecha o modal quando usuário clicar em qualquer lugar na janela do browser
        janelaClick(event) {
            if (event.target == myModal) {
                myModal.style.display = "none";
            }
        }
    },
    created: function() {
        window.addEventListener('click',this.janelaClick);
    },
    destroyed: function() {
        window.removeEventListener('click', this.janelaClick);
    },props: [ 'myHeader', 'myFooter']
}
</script>

<style scoped>
/* Botao Fechar */
    .close:hover,
    .close:focus {
        color: black;
        text-decoration: none;
        cursor: pointer;
    }

    /* Cabecalho do Modal */
    .modal-header {
        padding: 2px 16px;
        background-color: #5cb85c;
        color: white;
    }

    /* Janela Modal (background) */
    .modal-body {padding: 2px 16px;}

    /* Rodape do Modal */
    .modal-footer {
        padding: 2px 16px;
        background-color: #5cb85c;
        color: white;
    }

    /* Conteudo da janela Modal */
    .modal-content {
        position: relative;
        background-color: #fefefe;
        margin: auto;
        padding: 0;
        border: 1px solid #888;
        width: 80%;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2),0 6px 20px 0 rgba(0,0,0,0.19);
        animation-name: animatetop;
        animation-duration: 0.4s
    }

    /* Definicoes de animacao */
    @keyframes animatetop {
        from {top: -300px; opacity: 0}
        to {top: 0; opacity: 1}
    }
</style>
