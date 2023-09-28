// vars/msnetDependencies.groovy
def call() {
    MSBUILD_INSTALLER = "https://aka.ms/vs/17/release/vs_BuildTools.exe"
    MSBUILD_COMPONENTS = "--add Microsoft.Component.ClickOnce.MSBuild --add Microsoft.Net.Component.4.8.SDK --add Microsoft.NetCore.Component.Runtime.6.0 --add Microsoft.NetCore.Component.Runtime.7.0 --add Microsoft.NetCore.Component.SDK --add Microsoft.VisualStudio.Component.NuGet.BuildTools --add Microsoft.VisualStudio.Component.WebDeploy --add Microsoft.VisualStudio.Web.BuildTools.ComponentGroup --add Microsoft.VisualStudio.Workload.MSBuildTools"    
    echo "Installing MSBuild and Donet Framework"
    bat "curl -fSLo vs_BuildTools.exe ${MSBUILD_INSTALLER}"
    bat "start /w vs_BuildTools.exe --installPath \"${tool 'MSBuild2017'}\" ${MSBUILD_COMPONENTS} --quiet --norestart --nocache --wait"

    powershell '''
        $ErrorActionPreference = 'Stop';
        $ProgressPreference = 'SilentlyContinue';
        @('4.0', '4.5.2', '4.6.2', '4.7.2', '4.8', '4.8.1') | % {
            Invoke-WebRequest -UseBasicParsing -Uri https://dotnetbinaries.blob.core.windows.net/referenceassemblies/v${_}.zip -OutFile referenceassemblies.zip;
            Expand-Archive referenceassemblies.zip -DestinationPath "C:\\Program Files (x86)\\Reference Assemblies\\Microsoft\\Framework\\.NETFramework";
            Remove-Item -Force referenceassemblies.zip;
        }
    '''
}
