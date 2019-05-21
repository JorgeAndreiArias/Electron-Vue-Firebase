<template>
  <div class="about">
    <h1>Insert data</h1>
    <input placeholder="Tittle" v-model="titulo"/>
    <textarea placeholder="Data" v-model="contenido" cols="30" rows="10"></textarea>
    <input type="button" value="Create Document" v-on:click="createDocument">
  </div>
</template>

<script>
import {docx, Document, Packer, Paragraph, TextRun }  from "docx"
import * as fs from "fs";
export default {
  data: function () {
    return{
      contenido: null,
      titulo: null,
    }
  },
  methods: {
    createDocument(){
      var doc = new Document();
      var tittle = new Paragraph(this.titulo).center().title();
      var paragraph =  new Paragraph(this.contenido).justified().heading5();
      doc.addParagraph(tittle);
      doc.addParagraph(paragraph);
      var packer = new Packer();
      packer.toBuffer(doc).then((buffer) => {
          fs.writeFileSync("My First Document.docx", buffer);
      });
    },
  }
}
</script>


