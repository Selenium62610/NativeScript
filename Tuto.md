# Bienvenue au tuto de Nativescript!
Tout d'abord pour ce tuto vous allez devoir installer sur votre portable l'application **NativeScript Playground** et **NativeScript Preview**. Ces deux outils vont nous permettre de lire le **QRCODE** généré par par Nativescript afin de pouvoir voir et débugger notre application.
Ensuite vous devrez installer sur votre machine l'interface de ligne de commande. Pour cela vous devrez tout d'abord vous assurez d'avoir **NodeJs** sur votre machine, enfin ouvrez un terminal et lancez la commande suivante:
```
npm install -g nativescript
```
Pour vérifier si l'installation est fonctionnel vous pouvez lancez la commande suivante:
```
tns
```
Une fenêtre devrait alors s'afficher dans votre terminal.

Félicitation NativeScript est désormais fonctionnel sur votre machine.


# Créer votre première application

Afin de créer notre première application NativeScript nous devons utiliser la commande suivante qui permet d'initialiser un répertoire
```
tns create Tuto --template tns-template-blank
```
Tuto étant le nom de l'application que nous créons et l'option **- -template** qui permet de prédéfinir le template utilisé, dans notre cas celui ci sera vide.

La commande create peut prendre quelques minutes, puisque NativeScript à besoin de télécharger quelques dépendances tout en initialisant l'environnement de travail.

Lorsque la commande prend fin, vous pouvez accéder dans le répertoire qui vient d'être créé
```
cd Tuto
```

## Jeter un premier oeil à l'application

Afin d'avoir un aperçu de ce que nous créons nous devons pouvoir voir ce que vous faisons, pour ce faire **NativeScript** est capable de produire un **QR Code** qui sera lu par l'application que nous avons téléchargé précédemment.

Dans un terminal vous pouvez écrire la commande suivante:
(agrandissez votre terminal)
```
tns preview
```

Si tout ce passe bien, vous ne devriez pas tarder à voir un **QR Code** apparaître dans votre terminal.
![Un QR Code](https://lh3.googleusercontent.com/eJxhUHOQD41SHf5Zbk1ntcteiN3YbI8Y6b3MXLoFFwfPqf7y9I38AcPjnav_7u2Bv-09FrPEpT4 "Test")

Vous pouvez maintenant vous emparez de votre portable et lancer l'application **NativeScriptPlayground**, appuyez sur le QR Code au centre de l'écran afin de permettre le scan et fixer le QR Code de votre terminal.

![enter image description here](https://lh3.googleusercontent.com/8BxP98dlGKQFwXGT4BAdkuzi2nnyK9X01d2xFgjuanUNWy4JRx8Tp55VXiVnoILWUNlZFFWJsaQ)![enter image description here](https://lh3.googleusercontent.com/P_rZQaHd8dqoUTP2VAFUAgKFF-OyU8hgUIlX7vA9DzsyO071jSoDcpZrY3Q7GcfEPDMAX3abLKs)

De plus en fonction de votre os (Android ou Iphone) le rendu sera différents.

Enfin si vous revenez sur votre terminal vous pourrez constater que le _tns preview_ ne finit jamais. En effet dorénavant la commande surveille tout changement dans le projet et se rafraîchis lors d'un changement afin de pouvoir constater les changement immédiatement.

## Modifier le répertoire **home**

Vous pouvez maintenant ouvrir le projet dans votre IDE ou éditeur de texte préféré.

Vous devriez avoir quelque chose qui ressemble à ça: 

![enter image description here](https://lh3.googleusercontent.com/_M3R5sbsm-1zfWTDmLzLCS2UQvHNxAw_XDKQKal9GXd4N3dRyyO6z419UkRJq-YcPng6BWlRhOU)
Vous devez disposer de différents fichiers dans le répertoire _App_ ses derniers permettent de gérer la page qui sera affichés lorsque l'application sera affichés. On peut lire sur _app-root.xml_ que ce dernier initialise sa page par défaut comme étant _home-page_ dans le dossier **home**.

Si nous jetons un oeil à _home-page.xml_on remarque que ce fichier contient bien la barre d'action et le texte présent sur notre téléphone.
![enter image description here](https://lh3.googleusercontent.com/3042ldp1PHdZrWNuobPBfmLskDjB3vx1AQvvrEu0NlwziFErHtsLHV2iJTHV5qc_Fhl-gc76jCk)
## Créer le dossier login

Ce sera le dossier dans lequel nous allons implémenter nos fichiers afin de créer une page de login/inscription, pour cela nous devons créer un dossier au même niveau que **home**. Ce répertoire contiendra un fichier xml, css et js prénommée "login-page." et enfin un modèle view du nom de "login-view-model.js".

![enter image description here](https://lh3.googleusercontent.com/55ZvDZiyreRzri0s_l94Z64xpfU5lY5qdMr9UIopcE_kkqyC_i5JYXrw_HjmK3TOOhs7wBkScKo)

Vous pouvez collez le texte suivant dans _login-page.js_:
```javascript
const  LoginViewModel  =  require("./login-view-model");

const  loginViewModel  =  new  LoginViewModel();

exports.pageLoaded  =  function (args) {
	const  page  =  args.object;
	page.bindingContext  =  loginViewModel;
}
```
Ce dernier permet de déclarer que la page login utilisera comme modèle _login-view_ et utilisera ses fonctions après le chargement de la page. Il faut maintenant remplir le module afin qu'il puisse renvoyer des informations.

```javascript
const  observableModule  =  require("tns-core-modules/data/observable");

function  LoginViewModel() {
		const  viewModel  =  observableModule.fromObject({
	});
	
	return  viewModel;
}

module.exports  =  LoginViewModel;
```
Enfin dans _login-page.xml_ on peut introduire les lignes suivantes:
```xml
<Page  loaded="pageLoaded"  class="page"  actionBarHidden="true"  xmlns="http://www.nativescript.org/tns.xsd">
</Page>
```

Ensuite pour pouvoir afficher notre nouvel page qui sera la première affichés puisqu'elle nous permettra de nous connecter nous devons modifier la valeur qui était présente dans _app-root.xml_:
```xml
<FramedefaultPage="login/login-page"></Frame>
```
Si vous jetez un coup d'oeil à votre portable celui ci devrait vous afficher.....une page blanche. 
>Vous aurez peut être besoin de relancez le _tns preview_ à cause des changements sur le model-view)


## Modifier la page de login

Nous allons donc modifier la page de login afin d'afficher quelque chose de plus attrayant qu'on fond blanc, pour cela nous pouvons commencer par afficher le titre de notre application et un message dans une entête:

```xml
<Page  loaded="pageLoaded"  actionBarHidden="true"  xmlns="http://www.nativescript.org/tns.xsd">

	<FlexboxLayout  class="page">
		<StackLayout>
			<AbsoluteLayout  class ="connexion-top">
				<Label  class="title"  text="Notre application"  />
				<Label  class="underTitle"  text="Bienvenue"/>
			</AbsoluteLayout>
		</StackLayout>
	</FlexboxLayout>

</Page>
```
Si vous regardez le rendu une petite boite contenant vos messages à dû apparaître, maintenant nous allons utiliser un nouvel layout, GridLayout qui permet d'organiser nos éléments sous forme de grille pour pouvoir placer nos autres éléments servant au login:

```xml
<GridLayout  rows="auto, auto, auto, auto, auto,auto,auto, auto"  col="50 ,50"  >
	<StackLayout class="input" row="0"  class="input-field">
		<label  text="Login"/>
		<TextField  text="email"  hint=""
			keyboardType="email"  autocorrect="false"
			autocapitalizationType="none"  returnKeyType="next"  />
	</StackLayout>
</GridLayout>
```
et le code css correspondant: 
```css
.input-field {
	margin-top: 20;
	margin-left: 30;
	margin-right: 30;
	flex-grow: 2;
	margin-bottom: 20;
}

.connexion-top{
    width: 100%;
    border-color: blueviolet;
    border-bottom-width : 1.5;
    height: 185;
    background-color: #8e7cc3;
}

.page {
    align-items: center;
    flex-direction: column;
}

.underTitle
{
  width: 100%;
  padding: 100;
  border-radius: 50%;
  text-align: center;
  font-size: 18;
  color: white;
}

.title
{
  width: 100%;
  border-radius: 50%;
  text-align: center;
  font-size: 25;
  color: white;
}
```

Nous avons maintenant un champs pour entrer notre login assez correct, mais maintenant il faudrait pouvoir récupérer les informations envoyé.

## Envoyer et récupérer des informations

Maintenant nous pouvons nous intéresser au _login-view-model_, celui ci nous permettra de stocker temporairement nos données et d'accéder à d'autres pages ainsi que d'implémenter diverses interactions entre l'utilisateur et l'application.

Tout d'abord nous pouvons ajouter une variable **email** dans laquelle sera stockée l'information de l'utilisateur: 
```js
const  observableModule  =  require("tns-core-modules/data/observable"); 

function  HomeViewModel() {
	const  viewModel  =  observableModule.fromObject({
		email:  "poussière@test.org",
});
	return  viewModel;
}
module.exports  =  HomeViewModel;
```

Il nous faut maintenant récupérer l'email et pouvoir le modifier à partir de la page _login_ pour se faire on modifie la page _login-page.xml_ en changeant le Textfield précédemment créé comme ceci:

```xml
<GridLayout  class="input"  rows="auto, auto, auto, auto, auto,auto,auto, auto"  col="50 ,50"  >
	<StackLayout  row="0"  class="input-field">
		<label  text="Login"/>
		<TextField  text="{{email}}"  hint=""
			keyboardType="email"  autocorrect="false"
			autocapitalizationType="none"  returnKeyType="next"  />
	</StackLayout>
</GridLayout>

<Button  text="Connexion"  tap="{{ submit }}" isEnabled="{{ !processing }}" class="btn-primary"  />
```
```css
.btn-primary {
	margin-left: 30;
	margin-right: 30;
	flex-grow: 2;
	margin: 30  5  15  5;
	background-color: #8e7cc3;
}
```
Comme en angular on utilise la notation {{ x }} pour récupérer des valeurs présentes dans le modèle view. Maintenant votre application devrait afficher dans le champs de texte l'information que vous avez renseignés précédemment.

De plus comme en Angular, nous pouvons rapidement utiliser des fonctions, ainsi dans le bouton que nous venons d'ajouter nous avons joint une fonction qui sera appelé lorsque le bouton sera cliqué.
```js
const  observableModule  =  require("tns-core-modules/data/observable");

function  HomeViewModel() {
	const  viewModel  =  observableModule.fromObject({
		email:  "poussière@test.org",

		submit() {
			console.log(this.email);
		},
	});
	return  viewModel;
}
module.exports  =  HomeViewModel;
```
Lorsque vous cliquez sur le bouton _connexion_, l'email correspondant devrait s'afficher dans votre console.
# Ajoutons de nouveaux éléments
Il faudrait maintenant ajoutez de nouveaux éléments à la page de login afin de la rendre plus réaliste et pour pouvoir rentrer plus d'informations, pour cela j'ajoute de nouveaux champs à ma grille dans **login-page.xml**

```xml
<Page  loaded="pageLoaded"  actionBarHidden="true"  xmlns="http://www.nativescript.org/tns.xsd">
	<ScrollView>
		<FlexboxLayout  class="page">
			<StackLayout>
				<AbsoluteLayout  class ="connexion-top">
					<Label  class="title"  text="Notre application"  />

					<Label  class="underTitle"  text="Bienvenue"/>
				</AbsoluteLayout>

				<GridLayout  class="input"  rows="auto, auto, auto, auto, auto,auto,auto, auto"  col="50 ,50"  >
					<StackLayout  row="0"  class="input-field">
						<label  text="Login"/>
						<TextField  text="{{email}}"  hint=""
							keyboardType="email"  autocorrect="false"
							autocapitalizationType="none"  returnKeyType="next"  />
					</StackLayout>
					
					<StackLayout  row="1"  class="input-field">
						<Label  text="Password"/>
						<TextField  id="password"  class="input"  text="{{ password }}"
						secure="true"  returnKeyType="{{ isLoggingIn ? 'done' : 'next' }}"  />
						<Label  class="hr-light"  />
					</StackLayout>

					<StackLayout  row="2"  class="input-field"  visibility="{{ !isLoggingIn ? 'visible' : 'collapse' }}">
						<Label  text="Confirmer votre mot de passe"/>
						<TextField  id="confirmPassword"  class="input"  text="{{ confirmPassword }}"  secure="true"  returnKeyType="done"  />
						<Label  class="hr-light"  />
					</StackLayout>
				</GridLayout>
				
				<Button  text="{{ isLoggingIn ? 'Connexion' : 'S incrire' }}"  tap="{{ submit }}"  isEnabled="{{ !processing }}"  class="btn-primary"  />

			</StackLayout>

			<label  text="Ou"/>

			<Label  class="login-label sign-up-label"  tap="{{ toggleForm }}">
				<FormattedString>
					<Span  text="{{ isLoggingIn ? 'Envie de vous inscrire?' : 'Retour à la page de login' }}"  />
				</FormattedString>
			</Label>
		</FlexboxLayout>
	</ScrollView>
</Page>
```
et dans le **model-view**:
```js
const  observableModule  =  require("tns-core-modules/data/observable");

function  HomeViewModel() {
	const  viewModel  =  observableModule.fromObject({
		email:  "poussière@test.org",
		password:  "password",
		confirmPassword:  "",
		isLoggingIn:  true,

		submit() {
			console.log(this.email);
		},

		//Lorsque l'on passe dans la phase d'inscription et vice versa
		toggleForm() {
			this.isLoggingIn  =  !this.isLoggingIn;
		},
	});
	return  viewModel;
}
module.exports  =  HomeViewModel;
```
Lorsque vous cliquez sur le _label_ en bas de page vous changez la valeur de _isLogginIn_ et vous pouvez ainsi voir les champs qui étaient devenu invisible lorsque cette valeur était différente.

## Changer de page

Nous avons dorénavant quelques éléments qui nous permettent de nous identifier, mais ce qu'il nous manque est maintenant un système pour vérifier que ceux ci sont correctes et plus important encore un moyen de changer de page.

Pour ce faire nous allons modifier la fonction **submit** pour qu'elle vérifie tout d'abord que les informations ne soient pas nul, puis qui nous redirigera vers la page home.

le code à insérer avec amour: 
```js
submit() {
	if (this.email.trim() ===  ""  ||  this.password.trim() ===  "") {
		alert("Veuillez rentrer une adresse mail et un mot de passe valide.");
		return;
	}
	
	this.set("processing", true);
	if (this.isLoggingIn) {
		this.login();
	}
},

login() {
	this.set("processing", false);
	topmost().navigate({
		moduleName:  "/home/home-page",
		clearHistory:  true
	});
},
```
>Vous devrez ajouter cette constante qui permet de changer plus simplement la frame:
```js
const  topmost  =  require("tns-core-modules/ui/frame").topmost;
```
Vous avez maintenant accès à la page _home_ que nous avions créé plus tôt, nous pouvons maintenant la modifier pour qu'elle répond à nos attentes
## Save a file

La barre que nous voyons en haut est une ActionBar est comme en Android, nous permet d'accéder rapidement à certains composant.

Pour finir nous allons juste implémenter un bouton permettant de nous déconnecter:

```xml
<Page navigatingTo="onNavigatingTo" xmlns="http://schemas.nativescript.org/tns.xsd">

	<ActionBar  title="Home">
		<NavigationButton  android.systemIcon="ic_menu_back"  tap="{{goBack}}"/>
	</ActionBar>
	
	<GridLayout>
		<!-- Add your page content here -->
	</GridLayout>
	
</Page>
```

et dans le _home-view-model_:
```js
const  observableModule  =  require("tns-core-modules/data/observable");
const  topmost  =  require("tns-core-modules/ui/frame").topmost;

function  HomeViewModel() {
	const  viewModel  =  observableModule.fromObject({

		goBack() {
			this.set("processing", false);
			topmost().navigate({
				moduleName:  "/login/login-page",
				clearHistory:  true
			});
		},
	});

	return  viewModel;
}

module.exports  =  HomeViewModel;
```
Voilà vous avez maintenant l'esquisse de votre interface, et pouvez maintenant en théorie ajoutez ce que vous voulez à l'aide des différents composants mis à votre disposition.
