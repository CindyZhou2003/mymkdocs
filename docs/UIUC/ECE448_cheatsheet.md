##### 🏛️ Foundations: Probability, Latent Variables & VAEs (L1-L5)

-   **Generative Goal (L1):** Learn $p_\theta(x) \approx p_{data}(x)$ to generate new samples. Data often on a low-dim manifold. Main families: VAEs, GANs, Flows, Diffusion.
-   **Probability & Bayes (L2):** Key terms: **Likelihood** $p(data|\theta)$, **Prior** $p(\theta)$, **Posterior** $p(\theta|data)$. **MLE:** Maximize $L(\theta) = \prod p(x_i|\theta)$ or $\sum \log p(x_i|\theta)$ .
-   **Latent Variables & EM (L2-L3):** For $\theta \rightarrow Z \rightarrow X$ with hidden $Z$. **EM Algorithm:** Iteratively finds $\theta$ maximizing $p(X|\theta)$. **E-Step:** Compute expected complete log-likelihood $Q(\theta|\theta^{(t)}) = E_{Z \sim p(Z|X, \theta^{(t)})} [\log p(X, Z | \theta)]$. **M-Step:** $\theta^{(t+1)} = \arg\max_\theta Q(\theta|\theta^{(t)})$.
-   **Autoencoders (AE) (L4):** Encoder $X \rightarrow Z$, Decoder $Z \rightarrow Y$. Minimize reconstruction loss $L_{reconst}$. Latent space $Z$ unstructured, bad for generation 7.
-   **VAEs (L4-L5):** Better for generation. Encoder $q_\phi(Z|X)$ maps to distribution. Decoder $p_\theta(X|Z)$. **ELBO** (Loss): Maximize $\mathbb{E}_{z \sim q_\phi(z|x)}[\log p_\theta(x|z)] - D_{KL}(q_\phi(z|x) || p(z))$. Balances reconstruction and regularization. Issues: Prior mismatch, posterior collapse. VQ-VAE uses discrete latents.

##### 💧 Diffusion Models: Core Concepts & Connections (L6-L10a)

-   **Core Idea (L6):** **Forward Process $q$:** Gradually add noise $x_0 \rightarrow x_T \sim \mathcal{N}(0, I)$. Can jump: $q(x_t|x_0) = \mathcal{N}(x_t; \sqrt{\bar{\alpha}_t}x_0, (1-\bar{\alpha}_t)I)$ 11. **Reverse Process $p_\theta$:** Learn to denoise $x_T \rightarrow x_0$ step-by-step .
-   **Connection to VAEs (L6):** Hierarchical VAE with fixed encoder $q$, learned decoder $p_\theta$. Latents $x_1..x_T$ same dim as $x_0$.
-   **Simplified Loss (L7-L8):** VDM ELBO simplifies. Training objective becomes predicting the added noise $\epsilon$ using $\epsilon_\theta(x_t, t)$: $L_{simple} = \mathbb{E}_{t, x_0, \epsilon} ||\epsilon - \epsilon_\theta(x_t, t)||^2$ . Equivalent to predicting $x_0$ or the **score**.
-   **Score Function (L9, L10a):** $\nabla_x \log p(x)$ points towards higher probability density.
-   **Langevin Dynamics (L9, L10a):** Sample from $p(x)$ using score: . **Annealed Langevin:** Apply Langevin at decreasing noise levels $\sigma_k > ... > \sigma_0$.
-   **Tweedie's Formula (L9, L10a):** Links score $\nabla_y \log p(y)$ to MMSE estimate $\mathbb{E}[x|y]$ for $y=x+n$, $n \sim \mathcal{N}(0, \sigma^2 I)$: $\mathbb{E}[x|y] = y + \sigma^2 \nabla_y \log p(y)$.
-   **Connecting the Dots (L10a):** Tweedie shows **denoising $\approx$ score prediction**. $\nabla \log p(x_t) = -\epsilon_0 / \sqrt{1-\bar{\alpha}_t}$. Training $\epsilon_\theta$ (denoiser) implicitly learns score $s_\theta$. Can then use score + Langevin (or reverse SDE) for sampling. DDPM uses specific noise schedule $\alpha_t$ vs. annealed $\sigma_k$.

##### ⚙️ Controlling, Evaluating & Applying Diffusion (L11-L15)

-   **Guidance (L11/10b):** Control generation based on condition $c$.

    -   **CBG:** $\nabla \log p(x_t|c) \approx \nabla \log p(x_t) + s \cdot \nabla \log p(c|x_t)$ 24.
    -   **CFG:** Train $\epsilon_\theta(x_t, c)$ with null token $\phi$. Infer: $\tilde{\epsilon}_\theta = \epsilon_\theta(x_t, \phi) + s \cdot (\epsilon_\theta(x_t, c) - \epsilon_\theta(x_t, \phi))$. Preferred.

-   **T2I & Evaluation (L12):** Use text embedding (often from **CLIP**) as $c$. **CLIP:** Learns shared embedding space via contrastive loss. **FID:** Quality/diversity. **CLIP Score:** Text alignment . **LDM:** Diffusion in latent space.

-   **Inverse Problems (L13-L14):** Recover $x$ from $y = \mathcal{A}(x)+n$. Goal: sample $p(x|y)$.

    -   **DPS:** Use diffusion prior $p(x)$, likelihood $p(y|x)$ guides. Approx. $\nabla \log p(y|x_t) \approx \nabla \log p(y|\hat{x}_0)$. General.
    -   **PiGDM:** For **linear** $\mathcal{A}$, Gaussian noise. Calculates $\nabla \log p(y|x_t)$ **exactly** using pseudo-inverse .

-   **Advanced Applications (L15):** Handling challenging $\mathcal{A}$.

    -   **ArrayDPS:** $\mathcal{A}$ **unknown** (audio mixing). EM approach.

    -   **CoGuide:** $\mathcal{A}$ **non-differentiable** (path planning). Uses **contrastive learning** & **surrogate likelihood**.

    -   **InPose:** $\mathcal{A}$ **non-linear** (kinematics). **Decomposes posterior** $p(x|y) \propto p(x)\prod p(y_i|x)$ .

        

        