# GPU Droplet Benchmark# GPU Droplet Benchmark# GPU Droplet Benchmark# GPU Droplet Benchmark



A GitHub Actions workflow for testing DigitalOcean droplet capacity by creating and destroying test droplets using `doctl`.



## 🚀 FeaturesA GitHub Actions workflow for testing DigitalOcean droplet capacity by creating and destroying test droplets using `doctl`.



- **Real capacity testing** by creating actual droplets

- **Automatic cleanup** in separate job to ensure droplets are destroyed

- **Comprehensive validation** of inputs (region, size, image, SSH keys)## 🚀 FeaturesA GitHub Actions workflow for testing DigitalOcean droplet capacity by creating and destroying test droplets.This repository contains tools and workflows for benchmarking DigitalOcean GPU droplets and checking droplet capacity across different regions.

- **SSH key name support** - use friendly names instead of IDs

- **Detailed reporting** with success/failure analysis



## 📋 How to Use- **Real capacity testing** by creating actual droplets## 🚀 Features



### 1. Setup- **Automatic cleanup** in separate job to ensure droplets are destroyed



Add your DigitalOcean API token as a repository secret:- **Comprehensive validation** of inputs (region, size, image, SSH keys)### GitHub Actions Workflows

- Go to **Settings** → **Secrets and variables** → **Actions**

- Create a new secret named `DIGITALOCEAN_ACCESS_TOKEN`- **Detailed reporting** with success/failure analysis

- Get your token from [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens)

This repository provides two different approaches to check DigitalOcean droplet capacity:

### 2. Get SSH Key Names

## 📋 How to Use

```bash

doctl compute ssh-key list#### 1. 🧪 **Real-time Capacity Tester** (Recommended)

```

### 1. Setup

### 3. Run the Workflow

**Workflow:** `Test DigitalOcean Droplet Capacity (Real-time)`

- Go to **Actions** tab → **GPU Droplet Benchmarking** → **Run workflow**

- Enter parameters:Add your DigitalOcean API token as a repository secret:

  - **Slug:** e.g., `s-1vcpu-1gb`, `g-2vcpu-8gb-nvidia-l4`

  - **Region:** e.g., `nyc3`, `sfo3`, `tor1`- Go to **Settings** → **Secrets and variables** → **Actions**Uses the same **"attempt-based detection"** method as the [DO-Solutions/slug-grabber](https://github.com/DO-Solutions/slug-grabber) but for one-time testing without provisioning.

  - **Image:** e.g., `ubuntu-22-04-x64`, `gpu-h100x8-base`

  - **SSH Keys:** comma-separated names from step 2 (e.g., `my-key,work-laptop`)- Create a new secret named `DIGITALOCEAN_ACCESS_TOKEN`



## 🏗️ Workflow Structure- Get your token from [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens)**How it works:**



The workflow consists of 3 jobs:1. 🧪 Attempts to create an actual test droplet



### Job 1: `create-droplet`### 2. Get SSH Key IDs2. ✅ If successful → Capacity is definitely available

- Validates all inputs (region, size, image, SSH key names)

- Converts SSH key names to IDs automatically3. 🧹 Immediately deletes the test droplet (no charges)

- Creates the test droplet using `doctl`

- Waits for droplet to become active```bash4. ❌ If failed → No capacity or configuration issue

- Outputs droplet ID and name for cleanup

doctl compute ssh-key list

### Job 2: `destroy-droplet`

- Runs **only if** droplet creation succeeded```**Benefits:**

- Uses `if: always()` to ensure cleanup even if other steps fail

- Destroys the test droplet- ✅ **Real-time accuracy** - Tests actual availability right now

- Verifies successful deletion

### 3. Run the Workflow- ✅ **Definitive results** - No guessing, actual API response

### Job 3: `summary`

- Generates comprehensive test results- ✅ **No charges** - Test droplet is deleted immediately

- Shows creation and cleanup status

- Provides manual cleanup commands if needed- Go to **Actions** tab → **Test Droplet Capacity** → **Run workflow**- ✅ **Detailed analysis** - Explains why creation failed



## 💡 Example Configurations- Enter parameters:



**Basic Test:**  - **Slug:** e.g., `s-1vcpu-1gb`, `g-2vcpu-8gb-nvidia-l4`#### 2. 📋 **Basic Capacity Checker**

```

Slug: s-1vcpu-1gb  - **Region:** e.g., `nyc3`, `sfo3`, `tor1`

Region: nyc3

Image: ubuntu-22-04-x64  - **Image:** e.g., `ubuntu-22-04-x64`, `gpu-h100x8-base`**Workflow:** `Check DigitalOcean Droplet Capacity`

SSH Keys: my-laptop-key

```  - **SSH Keys:** comma-separated IDs from step 2



**GPU Droplet Test:**Uses `doctl` to check configuration validity and general availability using DigitalOcean's metadata APIs.

```

Slug: g-2vcpu-8gb-nvidia-l4## 🏗️ Workflow Structure

Region: nyc3

Image: ubuntu-22-04-x64**Benefits:**

SSH Keys: work-key,personal-key

```The workflow consists of 3 jobs:- ✅ **Fast and lightweight**



**H100 GPU Test:**- ✅ **No API creation calls**

```

Slug: gpu-h100x8-640gb### Job 1: `create-droplet`- ⚠️ **Less accurate** - Can't guarantee real-time capacity

Region: tor1

Image: gpu-h100x8-base- Validates all inputs (region, size, image, SSH keys)

SSH Keys: gpu-workstation

```- Creates the test droplet using `doctl`---



## ✅ Success Criteria- Waits for droplet to become active



- ✅ **Available:** Droplet creates successfully → Capacity exists- Outputs droplet ID and name for cleanup#### Setup Instructions

- ❌ **Unavailable:** Creation fails → No capacity or config issue

- 🧹 **Clean:** Droplet is destroyed automatically



## 🔗 Resources### Job 2: `destroy-droplet`1. **Set up DigitalOcean Access Token**:



- [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens)- Runs **only if** droplet creation succeeded   - Go to your repository's Settings > Secrets and variables > Actions

- [doctl CLI Documentation](https://docs.digitalocean.com/reference/doctl/)

- [DigitalOcean Pricing](https://www.digitalocean.com/pricing)- Uses `if: always()` to ensure cleanup even if other steps fail   - Add a new repository secret named `DIGITALOCEAN_ACCESS_TOKEN`

- Destroys the test droplet   - Set the value to your DigitalOcean API token (get one from [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens))

- Verifies successful deletion

2. **Run a Workflow**:

### Job 3: `summary`   - Go to the "Actions" tab in your GitHub repository

- Generates comprehensive test results   - Select either workflow

- Shows creation and cleanup status   - Click "Run workflow"

- Provides manual cleanup commands if needed   - Enter the required parameters:

     - **Droplet slug**: e.g., `s-1vcpu-1gb`, `c-2`, `g-2vcpu-8gb-nvidia-l4`

## 💡 Example Configurations     - **Region**: e.g., `nyc1`, `nyc3`, `sfo3`, `tor1`

     - **Test Method**: `create-and-destroy` (recommended) or `api-check-only`

**Basic Test:**

```#### Common Droplet Slugs

Slug: s-1vcpu-1gb

Region: nyc3**GPU Droplets:**

Image: ubuntu-22-04-x64- `g-2vcpu-8gb-nvidia-l4` - 2 vCPUs, 8GB RAM, NVIDIA L4

SSH Keys: 123456- `g-4vcpu-16gb-nvidia-l4` - 4 vCPUs, 16GB RAM, NVIDIA L4

```- `g-8vcpu-32gb-nvidia-l4` - 8 vCPUs, 32GB RAM, NVIDIA L4



**GPU Droplet Test:****CPU-Optimized:**

```- `c-2` - 2 vCPUs, 4GB RAM

Slug: g-2vcpu-8gb-nvidia-l4- `c-4` - 4 vCPUs, 8GB RAM

Region: nyc3- `c-8` - 8 vCPUs, 16GB RAM

Image: ubuntu-22-04-x64

SSH Keys: 123456,789012**General Purpose:**

```- `s-1vcpu-1gb` - 1 vCPU, 1GB RAM

- `s-2vcpu-2gb` - 2 vCPUs, 2GB RAM

**H100 GPU Test:**- `s-4vcpu-8gb` - 4 vCPUs, 8GB RAM

```

Slug: gpu-h100x8-640gb#### Common Regions

Region: tor1

Image: gpu-h100x8-base- `nyc1`, `nyc3` - New York

SSH Keys: 123456- `sfo3` - San Francisco

```- `tor1` - Toronto

- `lon1` - London

## ✅ Success Criteria- `fra1` - Frankfurt

- `sgp1` - Singapore

- ✅ **Available:** Droplet creates successfully → Capacity exists- `blr1` - Bangalore

- ❌ **Unavailable:** Creation fails → No capacity or config issue

- 🧹 **Clean:** Droplet is destroyed automatically## � Technical Approach



## 🔗 Resources### Attempt-Based Detection vs API Queries



- [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens)**Traditional Approach (API Queries):**

- [doctl CLI Documentation](https://docs.digitalocean.com/reference/doctl/)- ❌ Can be stale or inaccurate

- [DigitalOcean Pricing](https://www.digitalocean.com/pricing)- ❌ Doesn't account for race conditions
- ❌ May not reflect real-time capacity constraints

**Our Approach (Attempt-Based Detection):**
- ✅ **Real-time accuracy** - Tests actual creation API
- ✅ **Race condition proof** - If it works, capacity exists
- ✅ **Comprehensive testing** - Validates entire creation pipeline
- ✅ **Immediate cleanup** - No resource waste or charges

### Inspired by DO-Solutions/slug-grabber

This implementation adapts the proven capacity detection logic from [DO-Solutions/slug-grabber](https://github.com/DO-Solutions/slug-grabber), which uses continuous monitoring and actual droplet creation attempts to detect availability windows for high-demand resources like GPU droplets.

**Key differences:**
- 🔄 **One-time vs Continuous**: Single test vs continuous monitoring
- 🧹 **No provisioning**: Immediately deletes test droplets
- 📊 **Analysis focus**: Detailed reporting vs automated provisioning

## �📚 Resources

- [DigitalOcean Availability Matrix](https://docs.digitalocean.com/products/platform/availability-matrix/)
- [DigitalOcean API Documentation](https://docs.digitalocean.com/reference/api/)
- [doctl CLI Documentation](https://docs.digitalocean.com/reference/doctl/)
- [DO-Solutions/slug-grabber](https://github.com/DO-Solutions/slug-grabber) - Automated droplet provisioning

## 🤝 Contributing

Feel free to submit issues and enhancement requests!