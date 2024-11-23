# **Kubernetes Troubleshooting: Debugging Pods and Cluster Issues**

Kubernetes is a powerful platform, but issues like failing pods, unresponsive services, or unexpected application behavior can arise. This guide summarizes essential commands and techniques to help troubleshoot common Kubernetes problems effectively.

## **Key Troubleshooting Steps**

### **1. Checking Pod Status**
- Use `kubectl get pods -n <namespace>` to view pod statuses.
- Look for issues like `CrashLoopBackOff` or `Error` in the status column.

### **2. Inspecting Pods**
- Use `kubectl describe pod <pod-name> -n <namespace>` for detailed insights into pod events, resource usage, and errors (e.g., image pull failures).

### **3. Viewing Logs**
- Check application logs with:
  - `kubectl logs <pod-name> -n <namespace>`
  - For multi-container pods: `kubectl logs <pod-name> -c <container-name> -n <namespace>`.

### **4. Debugging Inside Pods**
- Use `kubectl exec -it <pod-name> -n <namespace> -- /bin/sh` to access the container's shell and inspect logs, files, or network connectivity.

### **5. Troubleshooting Network Issues**
- Check services with `kubectl get svc -n <namespace>`.
- Verify the service type (ClusterIP, NodePort, LoadBalancer) and ensure correct port exposure.

### **6. Investigating Node Issues**
- Use `kubectl get nodes` to check node statuses.
- For detailed node health, use `kubectl describe node <node-name>`.

### **7. Viewing Cluster Events**
- List events with `kubectl get events -n <namespace>` to identify resource limits, pod failures, or other significant events.

### **8. Checking Resource Quotas and Limits**
- Use `kubectl get resourcequotas -n <namespace>` to view quotas.
- Ensure pods are not exceeding resource requests/limits defined in their YAML configuration.

### **9. Restarting or Deleting Pods**
- Restart or delete problematic pods with `kubectl delete pod <pod-name> -n <namespace>`. Kubernetes will recreate the pod if managed by a deployment or stateful set.

### **10. Advanced Debugging**
- Use `kubectl debug` (introduced in Kubernetes 1.18) to attach ephemeral debugging containers to running pods:
  - `kubectl debug -it <pod-name> --image=busybox -n <namespace>`.

---

## **Conclusion**
Mastering essential Kubernetes commands like `kubectl describe`, `kubectl logs`, and `kubectl exec` can simplify troubleshooting. With a solid understanding of your cluster’s architecture, you’ll be able to resolve issues quickly, ensuring optimal application performance and availability. Happy debugging!
