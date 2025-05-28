\documentclass[12pt]{article}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage[utf8]{inputenc}
\usepackage{booktabs}
\usepackage{siunitx}

\title{Nuclear Reactor Dynamics Model Documentation}
\author{Your Name}
\date{\today}

\begin{document}

\maketitle

\section{Model Overview}
This document describes the mathematical model for nuclear reactor dynamics based on the state-space representation shown in Figures ACMp4.png and ACMp4\_2.png. The model captures:
\begin{itemize}
    \item Point kinetics with delayed neutrons
    \item Fuel-coolant heat transfer dynamics
    \item Burnup accumulation
    \item Operational safety constraints
\end{itemize}

\section{State Vector Definition}
The system state is represented by:
\[
\mathbf{x} = \begin{bmatrix}
P & T_f & C & E & T_c
\end{bmatrix}^T
\]
where:
\begin{table}[h]
    \centering
    \begin{tabular}{ll}
        \toprule
        Symbol & Description \\
        \midrule
        $P$ & Core power (\si{\mega\watt}) \\
        $T_f$ & Average fuel temperature (\si{\celsius}) \\
        $C$ & Delayed-neutron precursor concentration (--) \\
        $E$ & Burn-up/energy tally (\si{\mega\watt\second}) \\
        $T_c$ & Hot-leg coolant temperature (\si{\celsius}) \\
        \bottomrule
    \end{tabular}
\end{table}

\section{Dynamic Equations}
\subsection{Power Dynamics}
\[
\dot{P} = \frac{\rho - \beta_{\text{mtx}}}{\Lambda}P + \lambda C
\]
where $\rho$ is reactivity and $\Lambda$ is neutron generation time.

\subsection{Fuel Temperature}
\[
\dot{T}_f = \frac{P}{m_f c_{pf}} - \frac{hA}{m_f c_{pf}}(T_f - T_c)
\]
with:
\begin{itemize}
    \item $m_f c_{pf} \approx \SIrange{1}{3}{\mega\joule\per\kelvin}$ (fuel heat capacity)
    \item $hA \approx \SIrange{40}{100}{\mega\watt\per\kelvin}$ (fuel-coolant conductance)
\end{itemize}

\subsection{Coolant Temperature}
\[
\dot{T}_c = \frac{hA}{m_c c_{pc}}(T_f - T_c) - \frac{\dot{m}}{m_c}(T_c - T_{\text{in}})
\]
where $m_c c_{pc} \approx \SIrange{0.5}{1}{\mega\joule\per\kelvin}$.

\section{Nonlinear Feedback Effects}
\subsection{Reactivity Feedback}
\[
\rho = \rho_{\text{prod}} + \alpha(T_f - T_0)
\]
where $\alpha$ is the Doppler coefficient.

\subsection{Delayed Neutron Fraction}
\[
\beta_{\text{mtx}} = \beta_0 - \gamma E
\]

\section{Safety Constraints}
\begin{table}[h]
    \centering
    \begin{tabular}{lll}
        \toprule
        ID & Constraint & Purpose \\
        \midrule
        C-1 & $T_f \leq \SI{800}{\celsius}$ & Fuel temperature limit \\
        C-2 & $|\Delta \rho_{\text{prod}}| \leq 0.1\% \Delta k/k\,\si{\per\second}$ & Rod-drive ramp rate \\
        C-3 & $E \leq E_{\text{max}}$ & Licensed burn-up \\
        C-4 & $\left|\frac{dP}{dt}\right| \leq 0.05 P_{\text{nom min}}^{-1}$ & Grid ramp-rate \\
        \bottomrule
    \end{tabular}
\end{table}

\section{Implementation Notes}
The model can be implemented in MATLAB/Python using ODE solvers:
\begin{verbatim}
function dxdt = reactor_ode(t, x, params)
    % Unpack parameters
    mf_cpf = params.mf_cpf;
    hA = params.hA;
    ...
    
    % Implement equations (e.g., x(1) = P)
    dxdt(1) = (rho - beta_mtx)/Lambda*x(1) + lambda*x(3);
    ...
end
\end{verbatim}

\begin{thebibliography}{9}
\bibitem{lamarsh} 
Lamarsh, J. R. (2001). 
\textit{Introduction to Nuclear Engineering}. 
Addison-Wesley.

\bibitem{duderstadt} 
Duderstadt, J. J., \& Hamilton, L. J. (1976). 
\textit{Nuclear Reactor Analysis}. 
Wiley.
\end{thebibliography}

\end{document}
