## 🛠️ Step 1: Create a Personal Access Token (PAT)

1. **Navigate to GitHub Settings**:

   * Go to [https://github.com/settings/tokens](https://github.com/settings/tokens).

2. **Generate a New Token**:

   * Click on **"Generate new token (classic)"**.

3. **Set Token Permissions**:

   * **Note**: If your repository is private, include the `repo` scope.
   * Select the following scopes:

     * `write:packages`
     * `read:packages`
     * `delete:packages` (optional, for deleting packages)

4. **Generate and Save the Token**:

   * Click **"Generate token"**.
   * **Important**: Copy and save the token securely. You won't be able to view it again.


## 🔐 Step 2: Authenticate Docker with GHCR

1. **Open Terminal**:

   * Use your preferred terminal or command prompt.

2. **Login to GHCR**:

   * Replace `YOUR_GITHUB_USERNAME` and `YOUR_PERSONAL_ACCESS_TOKEN` with your actual GitHub username and the token you just generated.

   ```bash
   echo YOUR_PERSONAL_ACCESS_TOKEN | docker login ghcr.io -u YOUR_GITHUB_USERNAME --password-stdin
   ```

   * Example:

   ```bash
   echo ghp_YourGeneratedTokenHere | docker login ghcr.io -u qu-cipher --password-stdin
   ```

   * If successful, you'll see: `Login Succeeded`.


## 🏷️ Step 3: Tag Your Docker Image

Assuming your local Docker image is named `<PROJECT_NAME>`, tag it for GHCR:

```bash
docker tag <PROJECT_NAME> ghcr.io/qu-cipher/<PROJECT_NAME>:latest
```

* This tags your image as `ghcr.io/qu-cipher/<PROJECT_NAME>` with the `latest` tag.
* You can replace `latest` with a specific version if desired, e.g., `v1.0.0`.


## 📤 Step 4: Push the Image to GHCR

Push your tagged image to GitHub Container Registry:

```bash
docker push ghcr.io/qu-cipher/<PROJECT_NAME>:latest
```

* Docker will upload your image layers to GHCR.
* Once completed, your image will be available at: [https://github.com/users/qu-cipher/packages/container/<PROJECT_NAME>](https://github.com/users/qu-cipher/packages/container/<PROJECT_NAME>)

---

## 🔄 Optional: Set Package Visibility

By default, packages are private. To make your image public:

1. **Navigate to the Package**:

   * Go to [https://github.com/users/qu-cipher/packages/container/<PROJECT_NAME>](https://github.com/users/qu-cipher/packages/container/<PROJECT_NAME>).

2. **Edit Package Settings**:

   * Click on **"Package settings"**.

3. **Change Visibility**:

   * Under **"Package visibility"**, select **"Public"**.

4. **Save Changes**:

   * Click **"Save changes"**.


## 🧪 Optional: Pull and Test the Image

To ensure everything works as expected, try pulling and running your image:

```bash
docker pull ghcr.io/qu-cipher/<PROJECT_NAME>:latest
docker run -p 8080:8080 ghcr.io/qu-cipher/<PROJECT_NAME>:latest
```

* Replace `8080` with the appropriate port your application uses.

---

If you prefer automating this process using GitHub Actions for continuous integration and deployment, feel free to ask, and I can guide you through setting that up as well.
