#include<iostream>
#include<fstream>
#include<string>
using namespace std;

class Echipa{
	static int nrEchipe;
	const int id;
	string denumire;
	int numar_jucatori;
	float valoare_lot;
public:
	friend ostream& operator<<(ostream& ob, Echipa& sursa){
		ob << "Denumire echipa: " << sursa.denumire << " nr juc " << 

sursa.numar_jucatori << " val lot " << sursa.valoare_lot << " RON" << endl;
		return ob;
	}

	
	friend ofstream& operator<<(ofstream& ob, Echipa& sursa){
		ob << sursa.denumire << endl;
		ob << sursa.numar_jucatori << endl;
		ob<< sursa.valoare_lot << endl;
		return ob;
	}


	
	friend ifstream &operator>>(ifstream& ob, Echipa&sursa){
		
		ob >> sursa.denumire;
		/*	char buffer[100];
		ob.getline(buffer, 100);

		sursa.denumire = buffer;
		ob >> sursa.numar_jucatori;

		ob >> sursa.valoare_lot;
		return ob;

	}

	friend istream &operator>>(istream& ob, Echipa&sursa){
		cout << "Da denumire echipa: ";
		ob >> sursa.denumire;
	/*	char buffer[100];
		ob.getline(buffer, 100);
		
		sursa.denumire = buffer;*/

		cout << "Da nr jucatori: ";
		ob >> sursa.numar_jucatori;

		cout << "Da val lot: ";
		ob >> sursa.valoare_lot;
		return ob;

	}

	Echipa() :id(nrEchipe){
		denumire = "Club anonim";
		numar_jucatori = 0;
		valoare_lot = 0;


		nrEchipe++;
	}

	Echipa(string d, int nrj, float vl) :id(nrEchipe){
	denumire = d;
	numar_jucatori = nrj;
	valoare_lot = vl;

	nrEchipe++;
	}

	Echipa(string d) :id(nrEchipe){
		denumire = d;
		numar_jucatori = 0;
		valoare_lot = 0;

		nrEchipe++;
	}
	Echipa(Echipa& e) :id(nrEchipe){
		denumire = e.denumire;
		numar_jucatori = e.numar_jucatori;
		valoare_lot = e.valoare_lot;

		nrEchipe++;
	}
	Echipa operator=(Echipa& e) {
		
		denumire = e.denumire;
		numar_jucatori = e.numar_jucatori;
		valoare_lot = e.valoare_lot;
		return*this;
	
	}

	void set_denumire(string den_nou){
		if (den_nou.length() > 3){
			denumire = den_nou;
		}
		else{
			cout << "Baga o denumire mai daca poti pls!" << endl;
		}

	}

	string get_denumire(){
		return denumire;
	}

	void set_numar_jucatori(int nrJucNou){
		if (nrJucNou > 0){
			numar_jucatori = nrJucNou;
		}
		else{
			throw "Eroare boss";
		}
	}

	int get_numar_jucatori(){
		return numar_jucatori;
	}

	bool operator> (Echipa& sursa){
		return this-> valoare_lot > sursa.valoare_lot;
	}

	bool operator!(){
		return numar_jucatori == 0;
	}
	
	operator float(){
		return valoare_lot / numar_jucatori;
	}

	Echipa operator++(int){
		Echipa copie = *this;
		numar_jucatori++;
		return copie;
	}

	double getValoareMedieJucatori(float dolar){
		
		return (valoare_lot / numar_jucatori) / dolar;
	}


	Echipa operator++(){
		numar_jucatori++;
		return*this;
	}


	void operator +=(float val){
		valoare_lot += val;
	}







};
int Echipa::nrEchipe = 0;







void main(){
	Echipa e1, e0;
	Echipa e2("Css5", 14, 3000);
	Echipa e3("Css6", 16, 3600);
	Echipa *pe = new Echipa("Steaua", 12, 6000);
	delete pe;

	//cin >> e0;
	//cout << e0;

	Echipa e4 = e2;
	//cout << e4;
	e1 = e3;
	//cout << e1;
	e1.set_denumire("Css4");
	//cout << e1.get_denumire() << endl;
	e1.set_numar_jucatori(10);
	//cout << e1.get_numar_jucatori() << endl;

	try{
		e1.set_numar_jucatori(-10);
	}
	catch (char* mesaj){
		//cout << mesaj << endl;
	}

	if (e1 > e0){
		//cout << e1.get_denumire() << "e mai mare ca e0" << endl;
	}
	else{
		cout << e0.get_denumire() << "e mai mare ca e1" << endl;
	}


	Echipa e10;
	if (!e10){
		//cout << e10.get_denumire() << " nu are jucatori" << endl;
	}
	
	Echipa e11;
	e11 =++ e10;
	e10 += 2000;
	//e10 += 200;


	//cout <<e11<< e10;
	double val_medie1 = e2.getValoareMedieJucatori(3.8);
	//cout << val_medie1 << endl;

	float val_medie = e2;
	//cout << val_medie << endl;


	Echipa citesteInObiect;
	ofstream outfis("echipa.txt", ios::out);
	//outfis << e2;
	ifstream infis("echipa.txt", ios::in);
	//infis >> citesteInObiect;
	//cout << citesteInObiect;

	int nrob = 3;
	Echipa vect[3] = { e2, e3, e4 };
	Echipa vect2[3];
	//outfis << nrob << endl;
	for (int i = 0; i < nrob; i++){
		outfis << vect[i];
	}
	
	for (int i = 0; i < nrob; i++){
		infis >> vect2[i];
	}
	for (int i = 0; i < nrob; i++){
		cout<< vect2[i];
	}

}
