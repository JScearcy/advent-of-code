use std::str::Split;

use crate::handler::{AdventSolution, SolveError, DayHandler};

{% set day_error = "Day" ~ day_num ~ "Error" -%}
{% set day_handler = "Day" ~ day_num ~ "Handler" -%}

#[derive(Debug)]
pub enum {{ day_error }} {}

impl Into<SolveError> for {{ day_error }} {
    fn into(self) -> SolveError {
        SolveError(format!("{{ day_error }}: {:?}", self))
    }
}

pub struct {{ day_handler }} {}
impl<'a> {{ day_handler }} {
    pub fn new() -> DayHandler<'a, &'a str> { DayHandler::new({{ day_handler }} {}) }
    pub fn solve_1(&self, _input_lines: Split<&str>) -> Result<String, {{ day_error }}> {
        todo!("Implement day {{ day_num }} challenge 1");
    }
    
    pub fn solve_2(&self, _input_lines: Split<&str>) -> Result<String, {{ day_error }}> {
        todo!("Implement day {{ day_num }} challenge 2");
    }
}

impl<'a> AdventSolution<&str> for {{ day_handler }} {
    fn get_day(&self) -> String { String::from("{{ day_num }}") }
    fn solve(&self, problem: &str, input: &str) -> Result<String, SolveError> {
        let input_lines = input.split("\n");
        let result = if problem == "1" {
            self.solve_1(input_lines)
        } else {
            self.solve_2(input_lines)
        };

        result.map_err(|e| e.into())
    }
}

#[cfg(test)]
mod tests {
    use crate::handler::AdventSolution;
    use super::{{ day_handler }};

    fn get_input<'a>() -> &'a str {
        todo!("Add test input to run tests")
    }

    #[test]
    fn get_day() {
        let handler = {{ day_handler }}::new();
        assert!(&handler.get_day() == "{{ day_num }}");
    }

    async fn solution(sol: &str) -> String {
        let handler = {{ day_handler }}::new();
        handler.solve(sol, get_input()).unwrap()
    }

    #[tokio::test]
    async fn solution_1() {
        let solution = solution("1").await;
        assert!(solution == String::from(""));
    }

    #[tokio::test]
    async fn solution_2() {
        let solution = solution("2").await;
        assert!(solution == String::from(""));
    }
}
