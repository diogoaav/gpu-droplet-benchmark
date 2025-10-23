# GPU Droplet Benchmark

This repository contains tools and workflows for benchmarking DigitalOcean GPU droplets and checking droplet capacity across different regions.

## 🚀 Features

### GitHub Actions Workflows

This repository provides two different approaches to check DigitalOcean droplet capacity:

#### 1. 🧪 **Real-time Capacity Tester** (Recommended)

**Workflow:** `Test DigitalOcean Droplet Capacity (Real-time)`

Uses the same **"attempt-based detection"** method as the [DO-Solutions/slug-grabber](https://github.com/DO-Solutions/slug-grabber) but for one-time testing without provisioning.

**How it works:**
1. 🧪 Attempts to create an actual test droplet
2. ✅ If successful → Capacity is definitely available
3. 🧹 Immediately deletes the test droplet (no charges)
4. ❌ If failed → No capacity or configuration issue

**Benefits:**
- ✅ **Real-time accuracy** - Tests actual availability right now
- ✅ **Definitive results** - No guessing, actual API response
- ✅ **No charges** - Test droplet is deleted immediately
- ✅ **Detailed analysis** - Explains why creation failed

#### 2. 📋 **Basic Capacity Checker**

**Workflow:** `Check DigitalOcean Droplet Capacity`

Uses `doctl` to check configuration validity and general availability using DigitalOcean's metadata APIs.

**Benefits:**
- ✅ **Fast and lightweight**
- ✅ **No API creation calls**
- ⚠️ **Less accurate** - Can't guarantee real-time capacity

---

#### Setup Instructions

1. **Set up DigitalOcean Access Token**:
   - Go to your repository's Settings > Secrets and variables > Actions
   - Add a new repository secret named `DIGITALOCEAN_ACCESS_TOKEN`
   - Set the value to your DigitalOcean API token (get one from [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens))

2. **Run a Workflow**:
   - Go to the "Actions" tab in your GitHub repository
   - Select either workflow
   - Click "Run workflow"
   - Enter the required parameters:
     - **Droplet slug**: e.g., `s-1vcpu-1gb`, `c-2`, `g-2vcpu-8gb-nvidia-l4`
     - **Region**: e.g., `nyc1`, `nyc3`, `sfo3`, `tor1`
     - **Test Method**: `create-and-destroy` (recommended) or `api-check-only`

#### Common Droplet Slugs

**GPU Droplets:**
- `g-2vcpu-8gb-nvidia-l4` - 2 vCPUs, 8GB RAM, NVIDIA L4
- `g-4vcpu-16gb-nvidia-l4` - 4 vCPUs, 16GB RAM, NVIDIA L4
- `g-8vcpu-32gb-nvidia-l4` - 8 vCPUs, 32GB RAM, NVIDIA L4

**CPU-Optimized:**
- `c-2` - 2 vCPUs, 4GB RAM
- `c-4` - 4 vCPUs, 8GB RAM
- `c-8` - 8 vCPUs, 16GB RAM

**General Purpose:**
- `s-1vcpu-1gb` - 1 vCPU, 1GB RAM
- `s-2vcpu-2gb` - 2 vCPUs, 2GB RAM
- `s-4vcpu-8gb` - 4 vCPUs, 8GB RAM

#### Common Regions

- `nyc1`, `nyc3` - New York
- `sfo3` - San Francisco
- `tor1` - Toronto
- `lon1` - London
- `fra1` - Frankfurt
- `sgp1` - Singapore
- `blr1` - Bangalore

## � Technical Approach

### Attempt-Based Detection vs API Queries

**Traditional Approach (API Queries):**
- ❌ Can be stale or inaccurate
- ❌ Doesn't account for race conditions
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