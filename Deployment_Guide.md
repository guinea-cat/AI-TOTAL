# 📖 GitHub Repository Deployment Guide (Docker Edition)

This guide details the complete process from "I found a cool project on GitHub" to "It's running on my computer". We will use the [Docker Getting Started Todo App](https://github.com/docker/getting-started-todo-app) as our example.

## 📋 Prerequisites (Preparation)

Before you start, ensure you have these two tools installed:
1.  **Git**: The tool to download code. [Download Git](https://git-scm.com/downloads)
2.  **Docker Desktop**: The tool to run the code. [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)

---

##  step 1: Download the Code (Clone)

We need to get the files from GitHub to your computer.

1.  **Open your folder**: Navigate to the folder where you want to store the project.
2.  **Open Terminal**: Right-click and select "Open in Terminal" (or standard PowerShell).
3.  **Run the command**:
    ```powershell
    git clone https://github.com/docker/getting-started-todo-app.git
    ```
    *This creates a new folder named `getting-started-todo-app` with all the project files.*

4.  **Enter the folder**:
    ```powershell
    cd getting-started-todo-app
    ```

---

## Step 2: Analyze the "Recipe" (Optional but Recommended)

Before running anything, look for a file named `compose.yaml` (or `docker-compose.yml`).
- This file is the **instructions** for Docker.
- It tells you what services will start (e.g., `mysql` database, `backend` API, `frontend` client).

---

## Step 3: Launch the Application (Deploy)

Now for the magic. You don't need to install Node.js, MySQL, or configure databases manually. Docker does it all.

1.  **Run the start command**:
    ```powershell
    docker compose up -d
    ```
    - `up`: Create and start containers.
    - `-d`: **Detached** mode (runs in the background so you can keep using your terminal).

    *You will see Docker downloading "layers" (images) and then "Building" the custom parts.*

2.  **Wait for completion**:
    Wait until you see lines like `Container getting-started-todo-app-mysql-1 Started`.

---

## Step 4: Verify it's Working

1.  **Check status**:
    ```powershell
    docker compose ps
    ```
    *Look for the "STATUS" column. It should say "Up" or "Running".*

2.  **Open in Browser**:
    - **Todo App**: [http://localhost](http://localhost)
    - **Database Management**: [http://db.localhost](http://db.localhost)

---

## Step 5: Stop the Application

When you are done, shut it down to save system resources.

1.  **Run the stop command**:
    ```powershell
    docker compose down
    ```
    *This stops and removes the containers, but your data (in volumes) is usually preserved.*

---

## 🆘 Common Troubleshooting

- **Port Conflict**: If it says "Bind for 0.0.0.0:80 failed: port is already allocated", another program (like Skype or another web server) is using port 80.
- **Docker not running**: Make sure Docker Desktop is open and the whale icon is visible in your taskbar.

停止 Docker 运行有多种方式，具体取决于你是想停止**整个项目**、**单个容器**，还是关闭**整个 Docker 程序**。

以下是几种常用的操作场景及命令：

---

### 1. 停止当前文件夹下的项目 (最常用)

如果你是通过 `docker compose up` 启动的，在项目根目录下运行以下命令：

* **停止并移除容器：**
```bash
docker compose down

```


*这会停止容器、移除它们，并清理相关的网络。这是最干净的退出方式。*
* **仅停止（不移除）：**
```bash
docker compose stop

```


*容器会进入 "Exited" 状态，但不会被删除，下次启动会更快。继续运行：`docker compose start`*

---

### 2. 停止正在运行的单个容器

如果你想针对特定的容器进行操作，可以先查看列表，再停止：

1. **查看运行中的容器：**
```bash
docker ps

```


你会看到一串 `CONTAINER ID` 或 `NAMES`。
2. **停止容器：**
```bash
docker stop <容器ID或名称>

```


*例如：`docker stop getting-started-todo-app-client-1*`

---

### 3. 强行终止（类似于“强制结束任务”）

如果某个容器死锁了，正常的 `stop` 命令没反应，可以使用 `kill`：

```bash
docker kill <容器ID或名称>

```

---

### 4. 彻底关闭 Docker 桌面版 (Windows/Mac)

如果你想完全释放系统资源（内存和 CPU）：

1. 找到任务栏右下角的 **Docker 图标**（鲸鱼样式的）。
2. 右键点击，选择 **"Quit Docker Desktop"**。

---

### 5. 快速清理所有容器

如果你想一键停止**所有**正在运行的 Docker 容器，可以使用这个组合命令：

```bash
docker stop $(docker ps -q)

```

**提示：** 在 VS Code 中，如果你是直接运行 `docker compose up`（没加 `-d`），直接在终端窗口按 **`Ctrl + C`** 也可以停止当前服务。

你想了解如何清理那些停止后占地方的镜像或缓存吗？