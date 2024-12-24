# King
Seu
// ==UserScript==
// @name         Login Automático
// @namespace    http://tampermonkey.net/
// @version      1.1
// @description  Preenchimento automático do login
// @author       GERSON CHINOCA
// @match        https://visa.vfsglobal.com/*
// @grant        none
// ==/UserScript==

(() => {
  'use strict';

  const defaultUrl = "https://visa.vfsglobal.com/ago/en/prt/login";

  if (location.href === defaultUrl) {
    function preencherCampos() {
      const email = document.querySelector("input#email[formcontrolname='username']:not(.d-none)");
      const senha = document.querySelector("input[formcontrolname='password']");

      if (email) {
        // Preenchimento do campo de e-mail
        email.value = "martinselidio262@gmail.com";
        email.classList.remove("ng-invalid");
        email.classList.add("ng-valid");
        email.dispatchEvent(new Event('input', { bubbles: true }));
        console.log("Campo de e-mail preenchido!");
      }

      if (senha) {
        // Preenchimento do campo de senha
        senha.value = "Lisabona@70";
        senha.classList.remove("ng-invalid");
        senha.classList.add("ng-valid");
        senha.dispatchEvent(new Event('input', { bubbles: true }));
        console.log("Campo de senha preenchido!");
      } else {
        console.log("Campo de senha não encontrado!");
      }
    }

    // MutationObserver para garantir carregamento dinâmico
    const observer = new MutationObserver(() => {
      const email = document.querySelector("input#email[formcontrolname='username']:not(.d-none)");
      const senha = document.querySelector("input[formcontrolname='password']");
      if (email && senha) {
        preencherCampos();
        observer.disconnect();
      }
    });

    observer.observe(document.body, { childList: true, subtree: true });
  } else {
    console.log("URL diferente. O script não foi executado.");
  }
})();
