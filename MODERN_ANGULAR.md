# Modern Angular Development (Angular 17+)

## 1. Standalone Components

```typescript
// video-editor.component.ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { VideoService } from './video.service';

@Component({
  selector: 'app-video-editor',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './video-editor.component.html'
})
export class VideoEditorComponent {
  videos$ = inject(VideoService).getVideos();
}
```

No modules needed. Just standalone components.

---

## 2. Signal API (Reactive State)

```typescript
import { signal, computed } from '@angular/core';

export class VideoStore {
  videos = signal<Video[]>([]);
  selectedId = signal<string | null>(null);
  
  selectedVideo = computed(() => 
    this.videos().find(v => v.id === this.selectedId())
  );

  addVideo(video: Video): void {
    this.videos.update(v => [...v, video]);
  }
}
```

Synchronous, fine-grained reactivity without subscriptions.

---

## 3. New Control Flow (@if, @for, @switch)

```html
<!-- Old way -->
<div *ngIf="loading">Loading...</div>
<div *ngFor="let video of videos">{{ video.title }}</div>

<!-- Modern way -->
@if (loading()) {
  <div>Loading...</div>
}

@for (video of videos(); track video.id) {
  <video-card [video]="video"></video-card>
} @empty {
  <div>No videos</div>
}
```

Cleaner, faster, better TypeScript support.

---

## 4. Inject Function (No Constructor)

```typescript
// Old
export class VideoService {
  constructor(private http: HttpClient) { }
}

// Modern
import { inject } from '@angular/core';

export class VideoService {
  private http = inject(HttpClient);
}
```

No constructor boilerplate.

---

## 5. Functional Guards

```typescript
import { inject } from '@angular/core';
import { Router } from '@angular/router';
import { AuthService } from './auth.service';

export const authGuard = (route, state) => {
  const auth = inject(AuthService);
  const router = inject(Router);

  return auth.isLoggedIn() ? true : router.parseUrl('/login');
};

// Usage in routes
const routes = [
  {
    path: 'admin',
    component: AdminComponent,
    canActivate: [authGuard]
  }
];
```

Simple functions, no class boilerplate.

---

## 6. Standalone Routing

```typescript
// app.routes.ts
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: 'editor',
    component: VideoEditorComponent
  },
  {
    path: 'player/:id',
    loadChildren: () => import('./player/player.routes')
      .then(m => m.PLAYER_ROUTES)
  }
];

// main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { provideRouter } from '@angular/router';
import { AppComponent } from './app.component';
import { routes } from './app.routes';

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)]
});
```

Routes as arrays, not modules.

---

## 7. Signals + Observables (Hybrid)

```typescript
import { toSignal, toObservable } from '@angular/core/rxjs-interop';

@Component({...})
export class VideoEditorComponent {
  private videoService = inject(VideoService);

  // Observable → Signal
  videos = toSignal(
    this.videoService.getVideos(),
    { initialValue: [] }
  );

  // Signal → Observable
  selectedId = signal<string | null>(null);
  selectedVideo$ = toObservable(this.selectedId);
}
```

Best of both worlds.

---

## 8. Deferred Loading (@defer)

```html
@defer (on viewport; prefetch on idle) {
  <app-heavy-component></app-heavy-component>
} @placeholder {
  <div>Loading...</div>
} @loading {
  <div>Component loading...</div>
} @error {
  <div>Failed to load</div>
}
```

Lazy load components automatically.

---

## Quick Setup

```typescript
// app.config.ts
import { ApplicationConfig } from '@angular/core';
import { provideRouter } from '@angular/router';
import { provideHttpClient, withXsrfProtection } from '@angular/common/http';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(routes),
    provideHttpClient(withXsrfProtection()),
    provideAnimations()
  ]
};

// main.ts
bootstrapApplication(AppComponent, appConfig);
```

---

## Minimal Project Structure

```
src/
├── app/
│   ├── features/
│   │   ├── editor/
│   │   │   └── editor.component.ts (standalone)
│   │   └── player/
│   │       └── player.component.ts (standalone)
│   ├── services/
│   │   └── video.store.ts
│   ├── guards/
│   │   └── auth.guard.ts
│   ├── app.routes.ts
│   ├── app.config.ts
│   ├── app.component.ts (standalone)
│   └── main.ts
└── index.html
```

---

## Key Takeaways

✅ No NgModules  
✅ Standalone components  
✅ Signal API for state  
✅ `@if`, `@for`, `@switch` control flow  
✅ `inject()` function  
✅ Functional guards  
✅ Routes as arrays  
✅ `bootstrapApplication()` instead of NgModule  
