
# EduTrack: AI-Powered Exam Platform (Full Documentation)

## 📦 Project Overview
**EduTrack** is an AI-enhanced learning and examination platform built with Angular, .NET Core Web API, and MongoDB. Users can register, take exams, and receive AI feedback via OpenAI.

## 🧱 Architecture Summary
- **Frontend**: Angular 15+
- **Backend**: ASP.NET Core 6 Web API
- **Database**: MongoDB Atlas or SQL Server
- **AI Feedback**: OpenAI GPT-4 (via API)

## 🔧 Modules
### 🔐 Auth Module
- User registration & login
- JWT authentication
- Auth guards for secure routes

### 🎯 Exam Module
- Display available exams
- Take MCQ-based tests
- Submit results and receive AI feedback

### 📊 Admin Module
- Create/edit exams
- Add/edit/delete questions

### 📜 History Module
- View past results
- Question-by-question breakdown

## 🖥 Frontend (Angular)

### ✅ Folder Structure
```
src/app/
├── core/            # Shared services (auth, api)
├── shared/          # Header, footer, pipes
├── auth/            # Login, Register
├── dashboard/       # User dashboard
├── exams/           # Exam logic
├── admin/           # Admin panel
└── result-history/  # Previous results
```

### ✅ Angular Routing
```ts
const routes: Routes = [
  { path: 'auth/login', component: LoginComponent },
  { path: 'auth/register', component: RegisterComponent },
  { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] },
  { path: 'exams', component: ExamListComponent, canActivate: [AuthGuard] },
  { path: 'exam/:id', component: ExamEngineComponent, canActivate: [AuthGuard] },
  { path: 'admin/manage', component: ManageExamsComponent, canActivate: [AdminGuard] },
  { path: 'results', component: ResultHistoryComponent, canActivate: [AuthGuard] }
];
```

### ✅ Sample UI Code
#### login.component.html
```html
<form (ngSubmit)="login()">
  <input type="email" [(ngModel)]="email" name="email" required placeholder="Email">
  <input type="password" [(ngModel)]="password" name="password" required placeholder="Password">
  <button type="submit">Login</button>
</form>
```

## 📡 Backend (.NET Core)

### ✅ Controllers
- **AuthController**
- **ExamController**
- **QuestionController**
- **ResultController**
- **AiFeedbackController**

### ✅ Sample Controller
```csharp
[HttpPost("register")]
public async Task<IActionResult> Register(RegisterDto dto)
{
    var result = await _authService.RegisterAsync(dto);
    return Ok(result);
}
```

### ✅ OpenAI Integration
```csharp
var request = new {
    model = "gpt-4",
    messages = new[] {
        new { role = "user", content = "Evaluate: " + answersJson }
    }
};
```

## 💽 Database Schema

### USERS
```json
{
  "_id": ObjectId,
  "name": "Dipankar",
  "email": "d@example.com",
  "passwordHash": "...",
  "role": "admin"
}
```

## 🚀 Deployment

### Frontend
- `ng build`
- Host via [Netlify](https://www.netlify.com/) or [Vercel](https://vercel.com/)

### Backend
- Deploy API on [Render](https://render.com/) or [Fly.io](https://fly.io/)
- Set environment variables: DB URI, OpenAI key

### MongoDB Atlas
- Create cluster, collections for Users, Exams, etc.
- Add IP whitelist and connect string

## 🧪 Testing

### Angular Unit Tests (Karma + Jasmine)
```ts
describe('LoginComponent', () => {
  it('should call login on submit', () => {
    spyOn(component, 'login');
    component.login();
    expect(component.login).toHaveBeenCalled();
  });
});
```

### .NET Unit Tests (xUnit)
```csharp
[Fact]
public async Task Register_ShouldCreateUser()
{
  var result = await _controller.Register(new RegisterDto { ... });
  Assert.IsType<OkObjectResult>(result);
}
```

## 🧩 Optional Features
- Leaderboard for top scorers
- PDF export of results
- Timer + pause/resume logic
- Category/tag-based filtering
- Admin dashboard analytics

## 🧾 API Docs (Swagger)
Install Swagger in `Program.cs`:
```csharp
builder.Services.AddSwaggerGen();
app.UseSwagger();
app.UseSwaggerUI();
```
Visit `https://your-api-url/swagger`

## 📎 Hosting + CI/CD
- GitHub + Actions for build/test deploy
- Setup `.env` for OpenAI and DB keys
- Deploy Angular → Vercel, API → Render

## 📚 Summary
You now have:
- ✅ Full UI + routing (Angular)
- ✅ Complete API structure + AI integration
- ✅ MongoDB-ready schema
- ✅ Deployment and testing ready
- ✅ Swagger API docs
