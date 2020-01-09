# Cod-JS-Tehnici-Web--Ciocolata
var btn_select = document.getElementById("exampleFormControlSelect");//adauga optiuni in butonul select
for( var i=3;i>0;i--)
{
	var option=document.createElement('option');
	option.text=i;
	btn_select.add(option);
}

document.getElementById("formControlRange").min = "1940";//minimul butonului range
document.getElementById("formControlRange").max = "2019";//maximul butonului range
document.getElementById("formControlRange").step="1";//pasul de crestere/scadere

function updateTextInput(val) {
          document.getElementById('textInput').value=val; //imi afiseaza valoarea din range
        }

var rezultat1=false, rezultat2=false;//variabile globale pt a salva mesajul de validitate a email-ului/parolei

//verific daca email-ul e valid
document.body.addEventListener("keypress", function(event1){
	var tasta=event1.keyCode;
			if(tasta==13)
		{
			var regex1=/^[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?$/;
			var email=document.getElementById("exampleInputEmail").value;
			var result1=regex1.test(email);
			//console.log(email);
			//console.log(result1);
			if(result1==false)
				alert("Adresa Email invalida!");
			else 
				{	rezultat1=result1;
					document.getElementById("exampleInputPassword").focus();
				}
		}
});

//verific daca parola e valida
document.body.addEventListener("keypress", function(event2){
	var tasta=event2.keyCode;
			if(tasta==13)
		{
			var regex2=/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$/;
			/* cel putin 8 caractere, o litera mare, o litera mica, un numar, un caracter special*/
			var passwordd=document.getElementById("exampleInputPassword").value;
			var result2=regex2.test(passwordd);
			//console.log(passwordd);
			//console.log(result2);
			if(result2==false)
				alert("Parola invalida");
			else 
				{	rezultat2=result2;
					document.getElementById("formControlRange").focus();
				}
		}
});

var check=document.getElementById("exampleCheck");
var btn1=document.getElementById("submit");
var btn2=document.getElementById("reset");

// butonul de check e bifat/nebifat
var bifat=check.checked;//check=bifat ca sa fie global
check.addEventListener("click", function(ClickCheck){
	
	if(bifat==true)
		bifat=false;
	else bifat=true;
})

var ok=true;

//buton submit apasat
btn1.addEventListener("click", function(ClickSubmit){
	
	//daca sunt campuri invalide la click se modifica butonul de submit
	if( rezultat1==false || rezultat2==false || bifat==false)
	{	
		console.log(rezultat1);
		console.log(rezultat2);
		console.log(bifat);

		btn1.style.backgroundColor="black";
		btn1.innerHTML="Campuri invalide!";
		
		ok=false;
	}
	else/* daca toate campurile sunt valide */
		if(rezultat1==true && rezultat2==true && bifat==true)
			{	
				console.log(rezultat1);
				console.log(rezultat2);
				console.log(bifat);
				console.log(ok);
					
				btn1.style.backgroundColor="#007bff";
				btn1.innerHTML="Submit";
					
				//apel afisare date
				
				if(ok==true)// daca formularul a fost completat bine din prima si se apasa doar o data be buton
				{
					alert("Afisare date!");
					//obiect numit xhr care e de tipul XMLHttpRequest
					var xhr = new XMLHttpRequest();
					
					xhr.onload = function () {
					//xhr.status=ce status-code are cererea 
					if (xhr.status >= 200 && xhr.status < 300) {
					// Daca request-ul a fost facut cu succes
					console.log('Success!', xhr);
					console.log("Datele sunt:",JSON.parse(xhr.response));
					var users=JSON.parse(xhr.response);
					var date=document.getElementById("paragraf");
					date.innerHTML=users[0].name+", "+users[0].username+", "+users[0].email;
					document.getElementById("usersAjax").appendChild(date);
				
					}else // Fail
						console.log('The request failed!');
					};

					//request de tip GET catre jsonplacehoder
					xhr.open('GET', 'https://jsonplaceholder.typicode.com/users');
					xhr.send();	
				}
				else /* daca formularul nu a fost completat bine si se apasa de mai multe ori pe buton*/
				{	
					btn1.addEventListener("click", function(ClickSubmit2){
						
					alert("Afisare date!");
					//obiect numit xhr care e de tipul XMLHttpRequest
					var xhr = new XMLHttpRequest();
					
					xhr.onload = function () {
					//xhr.status=ce status-code are cererea 
					if (xhr.status >= 200 && xhr.status < 300) {
					// Daca request-ul a fost facut cu succes
					console.log('Success!', xhr);
					console.log("Datele sunt:",JSON.parse(xhr.response));
					var users=JSON.parse(xhr.response);
					var date=document.getElementById("paragraf");
					date.innerHTML=users[0].name+", "+users[0].username+", "+users[0].email;
					document.getElementById("usersAjax").appendChild(date);
					}else // Fail
						console.log('The request failed!');
					};

					//request de tip GET catre jsonplacehoder
					xhr.open('GET', 'https://jsonplaceholder.typicode.com/users');
					xhr.send();	
					});
				}
			}
});

//buton reset apasat
btn2.addEventListener("click", function(ClickReset){
	
	alert("Resetezi datele?");
	
});

var Lista=document.createElement("p");// creez paragraful cu lista tipurilor de ciocolata introduse
				
document.body.addEventListener("keypress", function(event3){
	var tasta=event3.keyCode;
			if(tasta==13)
			{	
				var input=document.getElementById("lista");
				var continut=input.value;// continutul listei
				var elemente=[];
				elemente.push(continut);//pun continutul listei in vector
				Lista.innerHTML+=elemente[0]+'<br>';//pun vectorul in paragraf
			}
});

var loc=document.getElementsByClassName("product")[2];
var btn1=document.createElement("button");
btn1.innerHTML="Afiseaza lista!";
loc.appendChild(btn1);
btn1.style.border="2px solid red";
btn1.style.backgroundColor="#00BFFF";

btn1.addEventListener("click", function(){
	
	document.getElementById("vector").appendChild(Lista);
});

//---------------------------------------------------------------------------

//creare paragraf
var loc1=document.getElementsByClassName("product")[0];
var paragraf=document.createElement("p1");
paragraf.innerHTML="Ciocolata a aparut in America Centrala acum circa 4000 de ani. Cacaua provine din fructul arborelui de cacao, fiind produsul final al unui proces ce implica prajirea si pisarea boabelor. Initial preparata ca un amestec intre pudra de cacao si o bautura, ciocolata de baut era folosita de indigeni in importante ritualuri religioase si sociale de-a lungul bazinului amazonian si America Centrala, inclusiv de mayasi si azteci. Boabele de cacao erau atat de valoroase incat in imperiul aztec erau folosite ca moneda.";
paragraf.style.color="#FFA07A";
paragraf.style.fontFamily="Raleway";
paragraf.style.fontSize="1.8vw";
paragraf.style.fontWeight="300";
loc1.appendChild(paragraf);

//stergere paragraf
var loc2=document.getElementsByClassName("product")[0];
var btn=document.createElement("button");
btn.innerHTML="Stergi acest paragraf?";
loc2.appendChild(btn);
btn.style.border="2px solid red";
btn.style.backgroundColor="#00BFFF";

btn.addEventListener("click", function(stergereParagraf){
	
	paragraf.remove();
});

//setInterval

console.log(Math.random());
var set=setInterval(function(){ 
	
	var r=Math.floor(Math.random()*256);
	var g=Math.floor(Math.random()*256);
	var b=Math.floor(Math.random()*256);
	
	var culoare="rgb("+r+","+g+","+b+")";
	
	console.log(culoare);
	
	document.body.style.backgroundColor=culoare;

},5000 )

//clearInterval
var loc3=document.getElementsByClassName("product")[2];
var btn2=document.createElement("button");
btn2.innerHTML="Aleg culoarea asta!";
loc3.appendChild(btn2);
btn2.style.border="2px solid red";
btn2.style.backgroundColor="#00BFFF";

btn2.addEventListener("click", function(){
	clearInterval(set);	
});

//setTimeout
var loc3=document.getElementsByClassName("product")[4];
var btn3=document.createElement("button");
btn3.innerHTML="Hello!";
loc3.appendChild(btn3);
btn3.style.border="2px solid red";
btn3.style.backgroundColor="#00BFFF";

btn3.addEventListener("click",function(event){
	
	var hei=setTimeout(alertF,3000);
});

function alertF(){ alert("Hello!")};
