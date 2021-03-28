[![Twitter Badge](https://img.shields.io/badge/chat-twitter-blue.svg)](https://twitter.com/ArrayLikeObj)

# Hacktober Fest 2020 Contribution #1

<p align="center">
  <img src="https://media3.giphy.com/media/KISloPw4Pz0Npa43vy/giphy.gif" alt="Demo gif">
</p>

## Concepts/ Tech
- OSS / Team Git collaboration
- Google Chrome Extension API
- CSS custom properties
- Pesisting state variables across chrome extension;
- Altering the options of a chrome extension via a popup (as opposed to going into the extension options).


## Contriubtions


<p align="center">
  <img src="https://i.gyazo.com/65a5ce84d85130f04ed4c114c92739a3.png" alt="Demo gif">
</p>

[Link to the closed issue](https://github.com/aquiles23/mangahost_navbar_fix/issues/9)


### Adding a toggle input
The issue on this repo was to find a way to enable and disable the nav bar that helps manga readers more easily navigate the mangahost2.com site. Usually changing the options/state of an extension would involve going into the options porition, which is cumbersome and most users don't know how to access it.

The solution was to add a toggle (similar to the ad-block extension) that would change the state of the extension. I used custom properties in CSS to make the design easily reusable in the future for this repo.
```
:root {
        --toggleContainerHeight: 30px;
	--toggleContainerWidth: 60px;
	--toggleContainerBg: linear-gradient(180deg, #2d2f39 0%, #1f2027 100%);
	--toggleCircleHeight: 24px;
	--toggleCircleWidth: 24px;
	--movementOffset: calc(var(--toggleContainerWidth) - var(--toggleCircleWidth) - 5px);
	--refreshButtonColor: #0707a8;
	--refreshButtonFontColor: #f1f1f1;
}
      
```

### Persiting the state of the option through a background script

Because the changing of the state is not done through the extension options directly every time the page reloads the state (navbar on or off) is deleted. I circumvent that with a Chrome Extension API that allows a background script to run whenever the extension is run, which lets me persist the state.
```
let extensionEnabled = false;
// Listen for changes to toggle/checkbox and send out extensionEnable
// to popup.js and remclass.js
chrome.extension.onMessage.addListener(function (
	request,
	sender,
	sendResponse
) {
	if (request.type === 'toggleOn') {
		extensionEnabled = true;
	}
	if (request.type === 'toggleOff') {
		extensionEnabled = false;
	}
	if (request.type === 'getToggleState') {
		sendResponse(extensionEnabled);
	}
});
```

--------------------------------------------------------------------------------
# Mangahost_navbar_fix

É feito para o site de leitura de mangas mangahost2.com (sua url muda com muita frequencia).

Um plugin de navegador com o intuito de ganhar pixels na imagem do manga escondendo a barra de navegação, que em minha opinião atrapalha a leitura.

## Exemplo

### Com o plugins

![com o plugin](./img/plugin_ativado.png)

### Sem o plugin

![sem o plugin](./img/plugin_desativado.png)

## Como usar

1. clone este repositório ou baixe como zip e extraia em algum lugar da sua maquina.

1. digite `chrome://extensions` na barra de navegação e precione enter (alternativamente pode ir no menu de extensões do seu navegador).

2. Habilite o modo desenvolvedor que fica no canto superior direito.

3. Clique no botão `Carregar sem compactação` e escolha a pasta deste projeto.

![Como usar](./img/load_extension.png)

Depois de seguir estes passos o plugin está pronto para uso, mais informações de instalações em https://developer.chrome.com/extensions/getstarted#manifest

Se encontrou um problema, abra uma issue descrevendo o problema em https://github.com/aquiles23/mangahost_navbar_fix/issues

Quer contribuir, escolha uma issue para trabalhar (ou crie uma) de acordo com o [guia de contribuição](./CONTRIBUTING.md), depois faça um pull request.