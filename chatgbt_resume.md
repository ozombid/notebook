## 🧩 Plan du cours Angular

1.  **Introduction à Angular**
    
2.  **Architecture et concepts clés**
    
3.  **Composants, Templates et Data Binding**
    
4.  **Directives**
    
5.  **Pipes**
    
6.  **Services et Injection de dépendances (DI)**
    
7.  **Routing et Navigation**
    
8.  **Formulaires (Template-driven et Reactive)**
    
9.  **HTTPClient et communication avec une API**
    
10.  **Observables et RxJS**
    
11.  **Modules et Lazy Loading**
    
12.  **Gestion d’état et optimisation**
    
13.  **Tests (Unitaires & e2e)**
    
14.  **Questions fréquentes d’entretien Angular**
    
15.  **Mini-projet récapitulatif**
    

----------

# 🧠 1. Introduction à Angular

**Angular** est un framework front-end développé par Google.  
Il sert à construire des **applications web SPA (Single Page Application)**.

🔹 Écrit en **TypeScript**  
🔹 Utilise une **architecture MVVM / Composants**  
🔹 Fournit tout : routing, formulaires, HTTP, tests, etc.

### ⚙️ Installation de base

```bash
npm install -g @angular/cli
ng new my-app
cd my-app
ng serve

```

> L’appli tourne sur `http://localhost:4200`

----------

# 🧱 2. Architecture d’une application Angular

Une app Angular est composée de :

-   **Modules** (`app.module.ts`)
    
-   **Composants** (`app.component.ts`)
    
-   **Templates HTML**
    
-   **Services**
    
-   **Routing**
    

### Exemple d’un composant

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello',
  templateUrl: './hello.component.html',
  styleUrls: ['./hello.component.css']
})
export class HelloComponent {
  name = 'Angular';
}

```

```html
<!-- hello.component.html -->
<h2>Hello {{ name }}!</h2>

```

----------

# 🔄 3. Data Binding & Templates

4 types de binding :

Type

Syntaxe

Description

Interpolation

`{{ variable }}`

Affiche des valeurs

Property binding

`[property]="expression"`

Modifie des propriétés du DOM

Event binding

`(event)="method()"`

Écoute les événements

Two-way binding

`[(ngModel)]="variable"`

Liaison bidirectionnelle

### Exemple :

```html
<input [(ngModel)]="username">
<p>Bonjour {{ username }}</p>

```

----------

# 🧭 4. Directives

Permettent de **modifier le DOM**.

### ➕ Directives structurelles

-   `*ngIf` → afficher/masquer
    
-   `*ngFor` → itérer sur une liste
    

```html
<p *ngIf="isLoggedIn">Bienvenue !</p>
<li *ngFor="let user of users">{{ user.name }}</li>

```

### 🎨 Directives d’attribut

-   `[ngClass]` / `[ngStyle]`
    
-   Créer ses propres directives avec `@Directive`.
    

----------

# ⚙️ 5. Pipes

Transforme les données dans le template :

```html
<p>{{ date | date:'short' }}</p>
<p>{{ price | currency:'EUR' }}</p>

```

✅ Personnalisation :

```ts
@Pipe({name: 'capitalize'})
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    return value.charAt(0).toUpperCase() + value.slice(1);
  }
}

```

----------

# 🔧 6. Services et Injection de dépendance (DI)

Les **services** contiennent la logique métier réutilisable.

```ts
@Injectable({ providedIn: 'root' })
export class UserService {
  getUsers() {
    return ['Alice', 'Bob', 'Charlie'];
  }
}

```

Puis tu l’injectes :

```ts
constructor(private userService: UserService) {}

```

----------

# 🛣️ 7. Routing et Navigation

Déclare les routes dans `app-routing.module.ts` :

```ts
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'user/:id', component: UserComponent }
];

```

```html
<a routerLink="/user/1">Voir utilisateur</a>
<router-outlet></router-outlet>

```

----------

# 🧾 8. Formulaires

### Template-driven

Facile à utiliser :

```html
<form #f="ngForm" (ngSubmit)="submit(f)">
  <input name="email" ngModel required>
</form>

```

### Reactive Forms

Plus puissants :

```ts
this.form = new FormGroup({
  email: new FormControl('', [Validators.required, Validators.email])
});

```

----------

# 🌐 9. HTTPClient

Pour consommer une API REST :

```ts
this.http.get<User[]>('https://api.example.com/users')
  .subscribe(data => this.users = data);

```

> Nécessite d’importer `HttpClientModule` dans ton `app.module.ts`.

----------

# ⚡ 10. RxJS et Observables

Angular utilise **RxJS** pour la gestion asynchrone.

Exemples :

```ts
this.userService.getUsers().subscribe(users => this.users = users);

```

Transformations :

```ts
this.http.get('/api/data').pipe(
  map(res => res.items),
  catchError(err => of([]))
)

```

----------

# 📦 11. Modules et Lazy Loading

Découpe ton app en **modules fonctionnels** :

```ts
@NgModule({
  declarations: [UserListComponent],
  imports: [CommonModule],
})
export class UserModule {}

```

Lazy loading :

```ts
{ path: 'users', loadChildren: () => import('./user/user.module').then(m => m.UserModule) }

```

----------

# 🧠 12. Gestion d’état & optimisation

-   Utiliser `BehaviorSubject` ou `NgRx` pour partager l’état global.
    
-   Optimiser les performances avec :
    
    -   `ChangeDetectionStrategy.OnPush`
        
    -   `trackBy` dans `*ngFor`
        
    -   Lazy loading des modules et des images
        

----------

# 🧪 13. Tests

### Unit tests (Jasmine + Karma)

```ts
it('should create component', () => {
  expect(component).toBeTruthy();
});

```

### e2e (Cypress / Playwright)

Teste le parcours utilisateur complet.

----------

# 💬 14. Questions fréquentes en entretien Angular

Thème

Exemple de question

Composants

Quelle est la différence entre `ngOnInit()` et le constructeur ?

Services

Comment fonctionne l’injection de dépendances ?

RxJS

Différence entre `Observable` et `Promise` ?

Change Detection

Qu’est-ce que `ChangeDetectionStrategy.OnPush` ?

Routing

Comment implémenter une route dynamique ?

Performance

Comment optimiser un `*ngFor` ?

Architecture

Différence entre Module, Component et Directive ?

Tests

Comment tester un composant dépendant d’un service ?

----------

# 🧑‍💻 15. Mini-projet pratique (à connaître)

**Projet typique en entretien** :

> Une mini application de gestion de tâches (To-Do list)

Concepts à démontrer :

-   Création de composants
    
-   Utilisation de `@Input()` et `@Output()`
    
-   Binding & Directives
    
-   Service pour gérer les tâches
    
-   Stockage local ou API mockée avec `HttpClient`
    

----------

Souhaites-tu que je te prépare :

1.  📘 **Une fiche de révision condensée** (10 pages max, idéale avant entretien),
    
2.  🧑‍💻 **Un mini-projet Angular complet avec code et explications**,
    
3.  🧠 **Une liste de questions/réponses d’entretien Angular (niveau junior → senior)** ?
    

Tu peux choisir **1, 2, ou 3**, ou plusieurs.
