# Aspire POCs

Generate Aspire manifest:

```powershell
$GitRoot = git rev-parse --show-toplevel
dotnet run --project "$GitRoot\Aspire-Starter\Aspire-Starter.AppHost\Aspire-Starter.AppHost.csproj" `
    -- `
    --publisher manifest `
    --output-path manifest.json
git hash-object "$GitRoot\Aspire-Starter\Aspire-Starter.AppHost\manifest.json"
```

Install Aspir8:

```powershell
dotnet tool install -g aspirate
```

Generate Kubernetes manifest:

```powershell
cd "$GitRoot\Aspire-Starter\Aspire-Starter.AppHost"

# Generate K8s manifest
aspirate generate

# Apply manifest to Kubernetes
aspirate apply

# Destroy the manifest
aspirate destroy
```

Generate Docker Compose manifest:

```powershell
# Generate Docker Compose
aspirate generate --output-format compose

cd "$GitRoot\Aspire-Starter\Aspire-Starter.AppHost\aspirate-output"
docker compose up -d
```
