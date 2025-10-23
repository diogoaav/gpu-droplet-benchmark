# GPU Droplet Benchmark

This repository contains tools and workflows for benchmarking DigitalOcean GPU droplets and checking droplet capacity across different regions.

## 🚀 Features

### GitHub Actions Workflow: Check Droplet Capacity

A workflow that allows you to check the availability of specific DigitalOcean droplet sizes in different regions using `doctl`.

#### How to Use

1. **Set up DigitalOcean Access Token**:
   - Go to your repository's Settings > Secrets and variables > Actions
   - Add a new repository secret named `DIGITALOCEAN_ACCESS_TOKEN`
   - Set the value to your DigitalOcean API token (get one from [DigitalOcean API Tokens](https://cloud.digitalocean.com/account/api/tokens))

2. **Run the Workflow**:
   - Go to the "Actions" tab in your GitHub repository
   - Select "Check DigitalOcean Droplet Capacity"
   - Click "Run workflow"
   - Enter the required parameters:
     - **Droplet slug**: e.g., `s-1vcpu-1gb`, `c-2`, `g-2vcpu-8gb-nvidia-l4`
     - **Region**: e.g., `nyc1`, `nyc3`, `sfo3`, `tor1`

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

## 📚 Resources

- [DigitalOcean Availability Matrix](https://docs.digitalocean.com/products/platform/availability-matrix/)
- [DigitalOcean API Documentation](https://docs.digitalocean.com/reference/api/)
- [doctl CLI Documentation](https://docs.digitalocean.com/reference/doctl/)

## 🤝 Contributing

Feel free to submit issues and enhancement requests!