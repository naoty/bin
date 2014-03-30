#!/usr/bin/env node

var marked = require("marked");
var renderer = new marked.Renderer();

renderer.code = function (code, header) {
    var metadata = header.split(":");
    var language = metadata[0];
    var filename = metadata[1];

    var text = "";
    text += '<div class="code-block">';
    if (filename) {
        text += '<div class="code-header"><span>';
        text += filename;
        text += "<span></div>";
    }
    text += '<div class="code-body"><pre>';
    text += code;
    text += "</pre></div></div>";
    return text;
};

process.stdin.resume();
process.stdin.setEncoding("utf8");

process.stdin.on("data", function (chunk) {
    console.log(marked(chunk, {renderer: renderer}));
});

